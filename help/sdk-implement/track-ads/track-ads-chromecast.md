---
title: Scopri come tenere traccia degli annunci in Chromecast
description: Implementa il tracciamento degli annunci nelle applicazioni Chromecast tramite Media SDK.
uuid: 7b1f584a-3472-416c-944c-5f5ea0ee5529
exl-id: 57465c42-b349-439d-b8d7-083b299a8c83
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# Tracciamento annunci in Chromecast{#track-ads-on-chromecast}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione tramite gli SDK 2.x. Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento degli annunci

| Nome costante | Descrizione   |
|---|---|
| `AdBreakStart` | Costante per il tracciamento dell&#39;evento di avvio AdBreak |
| `AdBreakComplete` | Costante per il tracciamento dell’evento AdBreak Complete |
| `AdStart` | Costante per il tracciamento dell’evento Ad Start |
| `AdComplete` | Costante per il tracciamento dell’evento Ad Complete |
| `AdSkip` | Costante per il tracciamento dell’evento Ad Skip |

## Passaggi di implementazione

1. Identifica quando inizia il limite di interruzione dell&#39;annuncio, incluso il pre-roll, e crea un `AdBreakObject` utilizzando le informazioni di interruzione dell&#39;annuncio.

   Creazione dell’oggetto di interruzione annuncio: [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdBreakObject)

   ```
   adBreakInfo = ADBMobile.media.createAdBreakObject("First Ad-Break", 1, AD_BREAK_START_TIME, playerName); 
   ```

1. Invoca `trackEvent()` con `AdBreakStart` nell&#39;istanza `MediaHeartbeat` per iniziare a tracciare l&#39;interruzione pubblicitaria: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, getAdBreakInfo());
   ```

1. Identifica quando inizia la risorsa dell’annuncio e crea un’istanza `AdObject` utilizzando le informazioni dell’annuncio.

   Creazione di oggetti annuncio: [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdObject)

   ```
   adInfo = ADBMobile.media.createAdObject("Sample ad", "001", 1, AD_LENGTH); 
   ```

1. Facoltativamente, allega metadati standard e/o di annunci alla sessione di tracciamento dei contenuti multimediali tramite variabili di dati di contesto.

   * **Metadati degli annunci standard -** Per i metadati standard degli annunci, crea un dizionario di coppie di valori chiave degli annunci standard utilizzando le chiavi per la piattaforma:
   * **Metadati annuncio personalizzati:** per i metadati personalizzati, crea un oggetto variabile per le variabili di dati personalizzate e compila i dati per la risorsa annuncio corrente:

1. Chiama `trackEvent()` con l&#39;evento `AdStart` per iniziare a tracciare la riproduzione dell&#39;annuncio.

   Includi un riferimento alla variabile di metadati personalizzata (o a un oggetto vuoto) come terzo parametro nella chiamata dell&#39;evento: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, getAdInfo(), adContextData);
   ```

1. Quando la riproduzione della risorsa dell’annuncio raggiunge la fine dell’annuncio, invoca `trackEvent()` con l’evento `AdComplete` : [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete); 
   ```

1. Se sono presenti annunci aggiuntivi all&#39;interno dello stesso `AdBreak`, ripeti nuovamente i passaggi da 3 a 6.
1. Al termine dell’interruzione pubblicitaria, utilizza l’evento `AdBreakComplete` per tenere traccia di: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete, getAdBreakInfo());
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con annunci pre-scorrimento](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) .
