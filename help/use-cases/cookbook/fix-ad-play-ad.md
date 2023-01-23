---
title: Risoluzione di main:play tra annunci
description: "Scopri come gestire le chiamate main:play inaspettate tra gli annunci."
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
exl-id: f27ce2ba-7584-4601-8837-d8316c641708
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '448'
ht-degree: 100%

---


# Gestione degli spazi tra annunci{#resolving-main-play-appearing-between-ads}

## PROBLEMA

In alcuni scenari di tracciamento degli annunci, si potrebbero verificare chiamate `main:play` inaspettate tra la fine di un annuncio e l’inizio di quello successivo. Se il ritardo tra la chiamata di completamento e la chiamata di inizio dell’annuncio successivo è superiore a 250 millisecondi, Media SDK tornerà a inviare chiamate `main:play`. Se si verifica il fallback su `main:play` durante l’interruzione pubblicitaria pre-roll, la metrica di inizio contenuto può essere impostata in anticipo.

Un gap tra annunci come descritto in precedenza viene interpretato da Media SDK come contenuto principale, perché non vi è sovrapposizione con alcun contenuto di annunci. Media SDK non dispone di informazioni sugli annunci e il lettore è in stato di riproduzione. Se non sono presenti informazioni sull’annuncio e lo stato del lettore è in riproduzione, per impostazione predefinita Media SDK attribuisce la durata del gap al contenuto principale. Non può attribuire la durata della riproduzione a informazioni sull’annuncio nulle.

## IDENTIFICAZIONE

Quando utilizzi Adobe Debug o uno sniffer di pacchetti di rete come Charles, se visualizzi le seguenti chiamate Heartbeat in questo ordine durante l’interruzione pubblicitaria pre-roll:

* Avvio sessione: `s:event:type=start` e `s:asset:type=main`
* Avvio annuncio: `s:event:type=start` e `s:asset:type=ad`
* Riproduzione annuncio: `s:event:type=play` e `s:asset:type=ad`
* Annuncio completato: `s:event:type=complete` e `s:asset:type=ad`
* Riproduzione contenuto principale: `s:event:type=play` e `s:asset:type=main` **(imprevisto)**

* Avvio annuncio: `s:event:type=start` e `s:asset:type=ad`
* Riproduzione annuncio: `s:event:type=play` e `s:asset:type=ad`
* Annuncio completato: `s:event:type=complete` e `s:asset:type=ad`
* Riproduzione contenuto principale: `s:event:type=play` e `s:asset:type=main` **(previsto)**

## RISOLUZIONE

***Ritarda l’attivazione della chiamata Annuncio completato.***

Gestisci il gap all’interno del lettore effettuando la chiamata `trackEvent:AdComplete` in ritardo per il primo annuncio, seguita immediatamente da `trackEvent:AdStart` per il secondo annuncio. L’app deve rimandare la chiamata dell’evento `AdComplete`, effettuandola dopo il termine del primo annuncio. Assicurati di effettuare una chiamata `trackEvent:AdComplete` per l’ultimo annuncio nell’interruzione pubblicitaria. Se il lettore è in grado di identificare che la risorsa dell’annuncio corrente è l’ultima dell’interruzione pubblicitaria, effettua immediatamente la chiamata `trackEvent:AdComplete`. Con questa risoluzione, meno di 1 secondo di tempo aggiuntivo trascorso sull’annuncio viene attribuito all’unità annuncio precedente.

**All’inizio dell’interruzione pubblicitaria, incluso pre-roll:**

* Crea l’istanza dell’oggetto `adBreak` per l’interruzione pubblicitaria, ad esempio: `adBreakObject`.

* Effettua la chiamata `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`

**A ogni avvio di risorse annuncio:**

* **Effettua la chiamata`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Effettua questa chiamata solo se l’annuncio precedente non è stato completato. Considera un valore booleano per mantenere uno stato “`isinAd`” per l’annuncio precedente.

* Crea l’istanza dell’oggetto annuncio per la risorsa, ad esempio: `adObject`
* Popola i metadati dell’annuncio, `adCustomMetadata`
* Effettua la chiamata `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`
* Effettua la chiamata `trackPlay()` se questo è il primo annuncio in un’interruzione pubblicitaria pre-roll.

**Per ogni risorsa annuncio completata:**

* **Non effettuare chiamate**

   >[!NOTE]
   >
   >Se l’applicazione sa che si tratta dell’ultimo annuncio nell’interruzione pubblicitaria, effettua una chiamata `trackEvent:AdComplete` e non impostare `trackEvent:AdComplete` in `trackEvent:AdBreakComplete`

**Quando l’annuncio viene saltato:**

* Effettua la chiamata `trackEvent(MediaHeartbeat.Event.AdSkip);`

**Al completamento dell’interruzione pubblicitaria:**

* **Effettua la chiamata`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Se questo passaggio è già stato eseguito in precedenza nell’ambito dell’ultima chiamata `trackEvent:AdComplete` allora può essere saltato.

* Effettua la chiamata `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`
