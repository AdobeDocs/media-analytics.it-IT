---
title: Scopri come tenere traccia degli annunci in Chromecast
description: Implementa il tracciamento degli annunci nelle applicazioni Chromecast tramite Media SDK.
uuid: 7b1f584a-3472-416c-944c-5f5ea0ee5529
exl-id: 57465c42-b349-439d-b8d7-083b299a8c83
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/iXdoMDwgSIK4zoz26eD3IUJ-7AkwU03GiADpb7rkpBk
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 357
ht-degree: 100%

---

# Tracciare gli annunci in Chromecast{#track-ads-on-chromecast}

Le istruzioni seguenti forniscono indicazioni per l’implementazione tramite gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/getting-started/download-sdks.md)

## Costanti di tracciamento degli annunci

| Nome costante | Descrizione   |
|---|---|
| `AdBreakStart` | Costante per il tracciamento dell’evento di avvio AdBreak |
| `AdBreakComplete` | Costante per il tracciamento dell’evento AdBreak Complete |
| `AdStart` | Costante per il tracciamento dell’evento Ad Start |
| `AdComplete` | Costante per il tracciamento dell’evento Ad Complete |
| `AdSkip` | Costante per il tracciamento dell’evento Ad Skip |

## Passaggi di implementazione

1. Identifica quando inizia il limite dell’interruzione dell’annuncio, incluso il pre-roll, e crea un `AdBreakObject` utilizzando le informazioni sull’interruzione dell’annuncio.

   Creazione dell’oggetto di interruzione pubblicitaria: [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdBreakObject)

   ```
   adBreakInfo = ADBMobile.media.createAdBreakObject("First Ad-Break", 1, AD_BREAK_START_TIME, playerName);
   ```

1. Chiamata `trackEvent()` con `AdBreakStart` nell’istanza `MediaHeartbeat` per iniziare a tracciare l’interruzione pubblicitaria: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, getAdBreakInfo());
   ```

1. Identifica quando inizia la risorsa dell’annuncio e crea un’istanza `AdObject` utilizzando le informazioni sull’annuncio.

   Creazione dell’oggetto annuncio: [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdObject)

   ```
   adInfo = ADBMobile.media.createAdObject("Sample ad", "001", 1, AD_LENGTH);
   ```

1. Facoltativamente, allega metadati standard e/o di annunci alla sessione di tracciamento dei contenuti multimediali tramite variabili di dati di contesto.

   * **Metadati standard per annunci**: per i metadati standard per annunci, crea un dizionario di coppie di valori chiave standard utilizzando le chiavi appropriate per la tua piattaforma:
   * **Metadati personalizzati per annunci**: per i metadati personalizzati, crea un oggetto variabile per le variabili di dati personalizzati e compila i dati per la risorsa annuncio corrente:

1. Chiamata `trackEvent()` con l’evento `AdStart` per iniziare a tenere traccia della riproduzione dell’annuncio.

   Includi un riferimento alla variabile di metadati personalizzata (o a un oggetto vuoto) come terzo parametro nella chiamata dell’evento: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, getAdInfo(), adContextData);
   ```

1. Quando la riproduzione della risorsa dell’annuncio raggiunge la fine dell’annuncio, chiama `trackEvent()` con l’evento `AdComplete`: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete);
   ```

1. Se ci sono altri annunci nello stesso `AdBreak`, ripeti di nuovo i passaggi da 3 a 6.
1. Al termine dell’interruzione pubblicitaria, utilizza l’evento `AdBreakComplete` da tracciare: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete, getAdBreakInfo());
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con annunci pre-roll](/help/use-cases/tracking-scenarios/vod-preroll-ads.md).
