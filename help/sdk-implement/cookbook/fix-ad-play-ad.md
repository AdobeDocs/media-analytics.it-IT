---
title: Risoluzione della riproduzione principale tra gli annunci
description: Come gestire le chiamate principali impreviste:play tra annunci.
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Risoluzione principale:riproduzione tra annunci{#resolving-main-play-appearing-between-ads}

## PROBLEMA

In alcuni scenari di monitoraggio degli annunci, si potrebbero verificare `main:play` chiamate che si verificano inaspettatamente tra la fine di un annuncio e l'inizio dell'annuncio successivo. Se il ritardo tra la chiamata ad complete e la successiva chiamata ad start è superiore a 250 millisecondi, Media SDK tornerà a inviare `main:play` le chiamate. Se questo fallback `main:play` si verifica durante un'interruzione di annuncio pre-roll, la metrica di inizio contenuto potrebbe essere impostata in anticipo.

Uno spazio vuoto tra gli annunci come descritto in precedenza viene interpretato dall’SDK di Media come contenuto principale, perché non vi è alcuna sovrapposizione con alcun contenuto pubblicitario. L’SDK per file multimediali non contiene informazioni sugli annunci e il lettore è in stato di riproduzione. Se non sono presenti informazioni pubblicitarie e lo stato del lettore è in fase di riproduzione, per impostazione predefinita Media SDK attribuisce la durata dello spazio vuoto al contenuto principale. Non può accreditare la durata della riproduzione a informazioni di annunci nulli.

## IDENTIFICAZIONE

Durante l'utilizzo di Adobe Debug o di un annusatore di pacchetti di rete come Charles, se durante un'interruzione di annuncio pre-roll vengono visualizzate le seguenti chiamate Heartbeat:

* Avvio sessione: `s:event:type=start` &amp; `s:asset:type=main`
* Inizio annuncio: `s:event:type=start` &amp; `s:asset:type=ad`
* Riproduzione annuncio: `s:event:type=play` &amp; `s:asset:type=ad`
* Annuncio completo: `s:event:type=complete` &amp; `s:asset:type=ad`
* Riproduzione contenuto principale: `s:event:type=play` &amp; `s:asset:type=main`(**imprevisto)**

* Inizio annuncio: `s:event:type=start` &amp; `s:asset:type=ad`
* Riproduzione annuncio: `s:event:type=play` &amp; `s:asset:type=ad`
* Annuncio completo: `s:event:type=complete` &amp; `s:asset:type=ad`
* Riproduzione contenuto principale: `s:event:type=play` &amp; `s:asset:type=main`**(previsto)**

## RISOLUZIONE

***Ritardo che attiva la chiamata Ad Complete.***

Gestire il gap dall'interno del lettore chiamando `trackEvent:AdComplete` tardi per il primo annuncio, seguito immediatamente da `trackEvent:AdStart` per il secondo annuncio. L'app deve essere sospesa quando si chiama l' `AdComplete` evento al termine del primo annuncio. Accertatevi di chiamare `trackEvent:AdComplete` l'ultimo annuncio nell'interruzione di annuncio. Se il lettore è in grado di identificare la risorsa dell’annuncio corrente come ultima nell’interruzione dell’annuncio, invoca `trackEvent:AdComplete` immediatamente. Con questa risoluzione, meno di un secondo del tempo aggiuntivo trascorso viene attribuito all’unità pubblicitaria precedente.

**Avvio dell'interruzione dell'annuncio, compreso il pre-roll:**

* Creare l'istanza dell' `adBreak` oggetto per l'interruzione annuncio; ad esempio, `adBreakObject`.

* Chiamata `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**Per ogni avvio di risorse di annunci:**

* **Chiama`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Chiama questo solo se l’annuncio precedente non è stato completato. Considerate un valore booleano per mantenere lo stato "`isinAd`" dell'annuncio precedente.

* Create l'istanza dell'oggetto annuncio per la risorsa annuncio: ad esempio, `adObject`.
* Compilate i metadati dell'annuncio, `adCustomMetadata`.
* Chiamata `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Chiama `trackPlay()` se si tratta del primo annuncio in un annuncio pre-roll.

**Per ogni risorsa annuncio completata:**

* **Non effettuare una chiamata**

   >[!NOTE]
   >
   >Se l'applicazione sa che si tratta dell'ultimo annuncio nell'interruzione dell'annuncio, chiama `trackEvent:AdComplete` qui e salta l'impostazione `trackEvent:AdComplete` nel `trackEvent:AdBreakComplete`

**Salta annuncio attivato:**

* Chiamata `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**Interruzione annuncio completata:**

* **Chiama`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Se questo passaggio è già stato eseguito come parte dell’ultima `trackEvent:AdComplete` chiamata, è possibile ignorarlo.

* Chiamata `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.

