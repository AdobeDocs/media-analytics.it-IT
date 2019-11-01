---
title: Tracciare annunci su Chromecast
description: Implementa il tracciamento degli annunci nelle applicazioni Chromecast tramite Media SDK.
uuid: 7b1f584a-3472-416c-944c-5f5ea0ee5529
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Tracciare annunci su Chromecast{#track-ads-on-chromecast}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione mediante gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento annunci

| Nome costante | Descrizione   |
|---|---|
| `AdBreakStart` | Costante per il tracciamento dell'evento AdBreak Start |
| `AdBreakComplete` | Costante per il tracciamento dell'evento AdBreak Complete |
| `AdStart` | Costante per il tracciamento dell'evento Ad Start |
| `AdComplete` | Costante per il tracciamento dell'evento Ad Complete |
| `AdSkip` | Costante per il tracciamento dell'evento Ad Skip |

## Passaggi di implementazione

1. Identificate quando inizia il limite di interruzione annuncio, incluso il pre-roll, e create un'interruzione `AdBreakObject` utilizzando le informazioni di interruzione annuncio.

   Creazione oggetto di interruzione annuncio: [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdBreakObject)

   ```
   adBreakInfo = ADBMobile.media.createAdBreakObject("First Ad-Break", 1, AD_BREAK_START_TIME, playerName); 
   ```

1. Chiama `trackEvent()` con `AdBreakStart` nell’ `MediaHeartbeat` istanza per iniziare a monitorare l’interruzione dell’annuncio: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, getAdBreakInfo());
   ```

1. Identifica quando inizia la risorsa dell'annuncio e crea un' `AdObject` istanza utilizzando le informazioni dell'annuncio.

   Creazione di oggetti annuncio: [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdObject)

   ```
   adInfo = ADBMobile.media.createAdObject("Sample ad", "001", 1, AD_LENGTH); 
   ```

1. Se necessario, allegate metadati standard e/o di annunci alla sessione di tracciamento dei supporti tramite le variabili dei dati contestuali.

   * **Metadati annuncio standard -** Per metadati annuncio standard, create un dizionario di coppie di valori di metadati di annunci standard utilizzando le chiavi per la vostra piattaforma:
   * **Metadati annuncio personalizzati - Per i metadati personalizzati,** create un oggetto variabile per le variabili di dati personalizzate e inserite i dati per la risorsa annuncio corrente:

1. Chiamate `trackEvent()` con l’ `AdStart` evento per iniziare a monitorare la riproduzione dell’annuncio.

   Includete un riferimento alla variabile di metadati personalizzata (o a un oggetto vuoto) come terzo parametro nella chiamata dell’evento: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, getAdInfo(), adContextData);
   ```

1. Quando la riproduzione della risorsa annuncio raggiunge la fine dell’annuncio, invoca `trackEvent()` con l’ `AdComplete` evento: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete); 
   ```

1. Se ci sono altri annunci all'interno dello stesso `AdBreak`, ripeti di nuovo i passaggi da 3 a 6.
1. Al termine dell'interruzione dell'annuncio, utilizzate l' `AdBreakComplete` evento per tenere traccia: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete, getAdBreakInfo());
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento della riproduzione [VOD con annunci](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) pre-roll.
