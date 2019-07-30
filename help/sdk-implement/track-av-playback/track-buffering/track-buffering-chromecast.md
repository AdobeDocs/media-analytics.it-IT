---
seo-title: Tenere traccia del buffering su Chromecast
title: Tenere traccia del buffering su Chromecast
uuid: f 6 fa 3 a 1 a-d 7 de -4293-bd 11-ebe 9 e 130 badd
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Track buffering on Chromecast{#track-buffering-on-chromecast}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione in tutti gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento del buffer


| Nome costante | Descrizione     |
|---|---|
| `BufferStart` | Costante per il tracciamento dell'evento di inizio del buffer |
| `BufferComplete` | Costante per il tracciamento dell'evento di completamento buffer |

## Implementare il buffering

1. Listen for the playback buffering events from media player, and on buffer start event notification, track buffering using the `BufferStart` event: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);
   ```

1. On buffer complete notification from the media player, track the end of buffering using the `BufferComplete` event: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
   ```

See the tracking scenario [VOD playback with buffering](/help/sdk-implement/tracking-scenarios/vod-buffering.md) for more information.
