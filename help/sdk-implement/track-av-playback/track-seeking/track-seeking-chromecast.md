---
seo-title: Tracciare la ricerca su Chromecast
title: Tracciare la ricerca su Chromecast
uuid: 8018 e 6 c 4-fed 9-4 de 7-9 eae-c 720 da 55 ad 8 c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Track seeking on Chromecast{#track-seeking-on-chromecast}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione in tutti gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento ricerca

| Nome costante | Descrizione     |
|---|---|
| `SeekStart` | Costante per il tracciamento dell'evento Seek Start. |
| `SeekComplete` | Costante per il tracciamento dell'evento Seek Complete. |

## Implementazione della ricerca

1. Listen for the playback seeking events from the media player, and on seek start event notification, track seeking using the `SeekStart` event: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekStart); 
   ```

1. On seek complete notification from the media player, track the end of seeking using the `SeekComplete` event: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekComplete); 
   ```

See the tracking scenario [VOD playback with seeking in the main content](/help/sdk-implement/tracking-scenarios/vod-seeking.md) for more information.
