---
seo-title: Tracciare la ricerca su Roku
title: Tracciare la ricerca su Roku
uuid: 0572252 b -397 f -4 aa 2-b 4 b 5-c 5346 b 75244 a
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Track seeking on Roku{#track-seeking-on-roku}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione in tutti gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento ricerca

| Nome costante | Descrizione     |
|---|---|
| `SeekStart` | Costante per il tracciamento dell'evento Seek Start. |
| `SeekComplete` | Costante per il tracciamento dell'evento Seek Complete. |

## Implementazione della ricerca

1. Listen for the playback seeking events from the media player, and on seek start event notification, track seeking using the `SeekStart` event.

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_START, seekInfo, seekContextData)
   ```

1. On seek complete notification from the media player, track the end of seeking using the `SeekComplete` event.

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_COMPLETE, seekInfo, seekContextData)
   ```

See the tracking scenario [VOD playback with seeking in the main content](/help/sdk-implement/tracking-scenarios/vod-seeking.md) for more information.
