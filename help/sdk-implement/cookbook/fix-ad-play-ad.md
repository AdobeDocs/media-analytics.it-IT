---
title: Risoluzione Della Riproduzione Principale Che Appare Tra Gli Annunci
description: '"Scopri come gestire le chiamate principali:play inaspettate tra gli annunci."'
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
exl-id: f27ce2ba-7584-4601-8837-d8316c641708
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---

# Risoluzione main:play tra annunci{#resolving-main-play-appearing-between-ads}

## PROBLEMA

In alcuni scenari di tracciamento degli annunci, potresti riscontrare chiamate `main:play` che si verificano inaspettatamente tra la fine di un annuncio e l’inizio dell’annuncio successivo. Se il ritardo tra la chiamata di completamento dell’annuncio e la chiamata di inizio dell’annuncio successiva è superiore a 250 millisecondi, Media SDK tornerà all’invio di chiamate `main:play` . Se il fallback a `main:play` si verifica durante un pre-roll ad break, la metrica di inizio contenuto può essere impostata in anticipo.

Un gap tra annunci come descritto sopra viene interpretato dall’SDK Media come contenuto principale, perché non c’è sovrapposizione con alcun contenuto pubblicitario. L’SDK di Media non dispone di informazioni sugli annunci impostate e il lettore è in stato di riproduzione. Se non sono presenti informazioni pubblicitarie e lo stato del lettore è in riproduzione, Media SDK attribuisce la durata del gap al contenuto principale per impostazione predefinita. Non può accreditare la durata della riproduzione verso informazioni di annunci nulli.

## IDENTIFICAZIONE

Quando utilizzi Adobe Debug o un packet sniffer di rete come Charles, se vedi le seguenti chiamate Heartbeat in questo ordine durante un pre-roll ad break:

* Avvio sessione: `s:event:type=start` &amp; `s:asset:type=main`
* Inizio annuncio: `s:event:type=start` &amp; `s:asset:type=ad`
* Ad Play: `s:event:type=play` &amp; `s:asset:type=ad`
* Annuncio completato: `s:event:type=complete` &amp; `s:asset:type=ad`
* Riproduzione contenuto principale: `s:event:type=play` &amp; `s:asset:type=main` **(imprevisto)**

* Inizio annuncio: `s:event:type=start` &amp; `s:asset:type=ad`
* Ad Play: `s:event:type=play` &amp; `s:asset:type=ad`
* Annuncio completato: `s:event:type=complete` &amp; `s:asset:type=ad`
* Riproduzione contenuto principale: `s:event:type=play` &amp; `s:asset:type=main` **(previsto)**

## RISOLUZIONE

***Ritardo nell’attivazione della chiamata Ad Complete.***

Gestisci lo spazio vuoto all&#39;interno del lettore richiamando `trackEvent:AdComplete` in ritardo per il primo annuncio, seguito immediatamente da `trackEvent:AdStart` per il secondo annuncio. Al termine del primo annuncio, l’app deve interrompere la chiamata dell’evento `AdComplete` . Assicurati di chiamare `trackEvent:AdComplete` per l&#39;ultimo annuncio nell&#39;interruzione pubblicitaria. Se il lettore è in grado di identificare che la risorsa dell&#39;annuncio corrente è la versione finale nell&#39;interruzione dell&#39;annuncio, chiama immediatamente `trackEvent:AdComplete` . Con questa risoluzione, meno di 1 secondo del tempo pubblicitario aggiuntivo viene attribuito all’unità pubblicitaria precedente.

**All&#39;inizio dell&#39;interruzione pubblicitaria, incluso il pre-roll:**

* Creare l&#39;istanza dell&#39;oggetto `adBreak` per l&#39;interruzione annuncio; ad esempio, `adBreakObject`.

* Chiamata `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**A ogni avvio di risorse pubblicitarie:**

* **Chiamata`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Chiamalo solo se l’annuncio precedente non è stato completato. Considera un valore booleano per mantenere lo stato &quot;`isinAd`&quot; per l’annuncio precedente.

* Crea l&#39;istanza dell&#39;oggetto annuncio per la risorsa annuncio: ad esempio, `adObject`.
* Compila i metadati dell’annuncio, `adCustomMetadata`.
* Chiamata `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Chiama `trackPlay()` se è il primo annuncio in un pre-roll ad break.

**Per ogni risorsa pubblicitaria completata:**

* **Non effettuare una chiamata**

   >[!NOTE]
   >
   >Se l&#39;applicazione sa che si tratta dell&#39;ultimo annuncio nell&#39;interruzione pubblicitaria, chiama `trackEvent:AdComplete` qui e salta l&#39;impostazione `trackEvent:AdComplete` in `trackEvent:AdBreakComplete`

**Salto annunci attivato:**

* Chiamata `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**Interruzione annuncio completata:**

* **Chiamata`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Se questo passaggio è già stato eseguito come parte dell’ultima chiamata `trackEvent:AdComplete` , puoi ignorarlo.

* Chiamata `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.
