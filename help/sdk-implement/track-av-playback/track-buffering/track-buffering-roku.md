---
seo-title: Tenere traccia del buffering su Roku
title: Tenere traccia del buffering su Roku
uuid: 6666 b 270-9 aa 3-42 ff -95 a 8-f 12502022 d 47
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Track buffering on Roku{#track-buffering-on-roku}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione in tutti gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../../sdk-implement/download-sdks.md)

## Costanti di tracciamento del buffer

| Nome costante | Descrizione     |
|---|---|
| `BufferStart` | Costante per il tracciamento dell'evento di inizio del buffer |
| `BufferComplete` | Costante per il tracciamento dell'evento di completamento buffer |

## Implementare il buffering

1. Listen for the playback buffering events from media player, and on buffer start event notification, track buffering using the `BufferStart` event.

   ```
   bufferInfo = {}
   bufferContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_BUFFER_START, bufferInfo, bufferContextData)
   ```

1. On buffer complete notification from the media player, track the end of buffering using the `BufferComplete` event.

   ```
   bufferInfo = {}
   bufferContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_BUFFER_COMPLETE, bufferInfo, bufferContextData)
   ```

See the tracking scenario [VOD playback with buffering](../../../sdk-implement/tracking-scenarios/vod-buffering.md) for more information.
