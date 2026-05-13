---
title: Spiegazione del tracciamento degli annunci
description: Panoramica dell’implementazione del tracciamento degli annunci con Media SDK.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PguxKIzAL95WbMl5c0yJq9rYSqZgOGbbAYtxOI4eVOs
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 510
ht-degree: 100%

---

# Panoramica{#overview}

Le istruzioni seguenti forniscono indicazioni per l’implementazione tramite gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/getting-started/download-sdks.md)

La riproduzione degli annunci include il tracciamento delle interruzioni, gli avvii, i completamenti e i salti degli annunci. Utilizza l’API del lettore multimediale per identificare gli eventi chiave del lettore e popolare le variabili di annuncio obbligatorie e facoltative.

## Eventi del lettore {#player-events}

### All’avvio dell’interruzione dell’annuncio

>[!NOTE]
>Inclusione del pre-roll

* Crea un’istanza dell’oggetto `adBreak` per l’interruzione dell’annuncio. Ad esempio, `adBreakObject`.

* Esegui la chiamata `trackEvent` per l’avvio dell’annuncio con `adBreakObject`.

### A ogni avvio di risorse annuncio

* Crea un’istanza di oggetto annuncio per la risorsa annuncio. Ad esempio, `adObject`.
* Popola i metadati dell’annuncio, `adCustomMetadata`.
* Esegui la chiamata `trackEvent` per l’avvio dell’annuncio.

### A ogni annuncio completato

* Esegui la chiamata `trackEvent` per l’annuncio completato.

### Al salto dell’annuncio

* Esegui la chiamata `trackEvent` per il salto dell’annuncio.

### All’interruzione annuncio completata

* Esegui la chiamata `trackEvent` per l’interruzione annuncio completata.

## Implementare il tracciamento degli annunci {#implement-ad-tracking}

### Costanti di tracciamento degli annunci

| Nome costante | Descrizione   |
|---|---|
| `AdBreakStart` | Costante per il tracciamento dell’evento di avvio AdBreak |
| `AdBreakComplete` | Costante per il tracciamento dell’evento AdBreak Complete |
| `AdStart` | Costante per il tracciamento dell’evento Ad Start |
| `AdComplete` | Costante per il tracciamento dell’evento Ad Complete |
| `AdSkip` | Costante per il tracciamento dell’evento Ad Skip |

### Passaggi di implementazione

1. Identifica quando inizia il limite dell’interruzione dell’annuncio, incluso il pre-roll, e crea un `AdBreakObject` utilizzando le informazioni sull’interruzione dell’annuncio.

   Specifihe di `AdBreakObject`:

   | Nome variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome dell’interruzione dell’annuncio come pre-roll, mid-roll e post-roll. | Sì |
   | `position` | La posizione numerica dell’interruzione pubblicitaria all’interno del contenuto, a partire da 1. | Sì |
   | `startTime` | Valore della testina di riproduzione all’inizio dell’interruzione pubblicitaria. | Sì |

1. Esegui la chiamata `trackEvent()` con `AdBreakStart` nell’istanza `MediaHeartbeat` per iniziare a tracciare l’interruzione dell’annuncio.

1. Identifica quando inizia l’annuncio e crea un’istanza `AdObject` utilizzando le informazioni sull’annuncio.

   Specifihe di `AdObject`:

   | Nome variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome descrittivo dell’annuncio. | Sì |
   | `adId` | Identificatore univoco per l’annuncio. | Sì |
   | `position` | La posizione numerica dell’annuncio all’interno dell’interruzione pubblicitaria, a partire da 1. | Sì |
   | `length` | Lunghezza annuncio | Sì |

1. Facoltativamente, allega metadati standard e/o di annunci alla sessione di tracciamento tramite variabili di dati di contesto.

   * **Metadati degli annunci standard:** per i metadati standard degli annunci, crea un dizionario di coppie di valori chiave di annunci standard utilizzando le chiavi per la piattaforma.
   * **Metadati degli annunci personalizzati:** per i metadati personalizzati, crea un oggetto variabile per le variabili di dati personalizzate e popolalo con i dati dell’annuncio corrente.

1. Esegui la chiamata `trackEvent()` con l’evento `AdStart` nell’istanza `MediaHeartbeat` per iniziare a tracciare la riproduzione dell’annuncio.

   Includi un riferimento alla variabile di metadati personalizzata (o a un oggetto vuoto) come terzo parametro nella chiamata dell’evento.

1. Quando la riproduzione dell’annuncio ne raggiunge la fine, esegui la chiamata `trackEvent()` con l’evento `AdComplete`.

1. Se la riproduzione dell’annuncio non è stata completata perché l’utente ha scelto di saltarlo, traccia l’evento `AdSkip`.
1. Se ci sono annunci aggiuntivi all’interno dello stesso `AdBreak`, ripeti di nuovo i passaggi da 3 a 7.
1. Al termine dell’interruzione pubblicitaria, utilizza l’evento `AdBreakComplete` per tracciarla.

>[!IMPORTANT]
>
>Assicurati di NON incrementare la testina di riproduzione del lettore di contenuti (`l:event:playhead`) durante la riproduzione dell’annuncio (`s:asset:type=ad`). Tale incremento influenzerebbe negativamente le metriche Tempo trascorso sul contenuto.

Il codice di esempio seguente utilizza l’SDK JavaScript 2.x per un lettore multimediale HTML5.

```js
/* Call on ad break start */

if (e.type == "ad break start") {
    var adBreakObject = MediaHeartbeat.createAdBreakObject("mid-roll", 2, 500);
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
};

/* Call on ad start */
if (e.type == "ad start") {
    var adObject = MediaHeartbeat.createAdObject("PepsiOne", "123456ab", 1, 30);
    /* Set custom context data */
    var adCustomMetadata = {
        affiliate:"Sample affiliate",
        campaign:"Sample ad campaign",
        creative:"Sample creative"
    }
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);
};

/* Call on ad complete */
if (e.type == "ad complete") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
};

/* Call on ad skip */
if (e.type == "ad skip") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
};

/* Call on ad break complete */
if (e.type == "ad break complete") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
};
```
