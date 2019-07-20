---
seo-title: Tracciare annunci su Chromecast
title: Tracciare annunci su Chromecast
uuid: 7 b 1 f 584 a -3472-416 c -944 c -5 f 5 ea 0 ee 5529
translation-type: tm+mt
source-git-commit: 2bf7cfd1e50309ce1ab8de0325d666ed209fbf5b

---


# Track ads on Chromecast{#track-ads-on-chromecast}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione tramite gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

## Costanti di tracciamento annunci

| Nome costante | Descrizione   |
|---|---|
| `AdBreakStart` | Costante per il tracciamento dell'evento adbreak Start |
| `AdBreakComplete` | Costante per il tracciamento dell'evento adbreak Complete |
| `AdStart` | Costante per il tracciamento dell'evento Ad Start |
| `AdComplete` | Costante per il tracciamento dell'evento Ad Complete |
| `AdSkip` | Costante per il tracciamento dell'evento Ad Skip |

## Passaggi di implementazione

1. Identify when the ad break boundary begins, including pre-roll, and create an `AdBreakObject` by using the ad break information.

   Ad break object creation: [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdBreakObject)

   ```
   adBreakInfo = ADBMobile.media.createAdBreakObject("First Ad-Break", 1, AD_BREAK_START_TIME, playerName); 
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, getAdBreakInfo());
   ```

1. Identify when the ad asset starts and create an `AdObject` instance using the ad information.

   Ad object creation: [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdObject)

   ```
   adInfo = ADBMobile.media.createAdObject("Sample ad", "001", 1, AD_LENGTH); 
   ```

1. Se necessario, allega metadati standard e/o annuncio alla sessione di tracciamento multimediale attraverso le variabili di dati di contesto.

   * **Metadati annunci standard -** Per i metadati degli annunci standard, create un dizionario di coppie di valori chiave per metadati pubblicitari standard utilizzando le chiavi per la piattaforma:
   * **Custom annunmetadati:** per i metadati personalizzati, crea un oggetto variabile per le variabili dati personalizzate e popolate i dati per la risorsa pubblicitaria corrente:

1. Call `trackEvent()` with the `AdStart` event to begin tracking the ad playback.

   Include a reference to your custom metadata variable (or an empty object) as the third parameter in the event call: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, getAdInfo(), adContextData);
   ```

1. When the ad asset playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete); 
   ```

1. If there are any additional ads within the same `AdBreak`, repeat steps 3 through 6 again.
1. When the ad break is complete, use the `AdBreakComplete` event to track: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete, getAdBreakInfo());
   ```

See the tracking scenario [VOD playback with pre-roll ads](../../sdk-implement/tracking-scenarios/vod-preroll-ads.md) for more information.
