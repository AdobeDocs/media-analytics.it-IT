---
seo-title: Tracciare la ricerca su Android
title: Tracciare la ricerca su Android
uuid: 65 addd 99-eebf -4 a 80-8 b 4 a-d 5 fbdff 8 ab 06
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Track seeking on Android{#track-seeking-on-android}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione in tutti gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento ricerca

| Nome costante | Descrizione     |
|---|---|
| `MediaHeartbeat.Event.SeekStart` | Costante per il tracciamento dell'evento Seek Start. |
| `MediaHeartbeat.Event.SeekComplete` | Costante per il tracciamento dell'evento Seek Complete. |

## Implementazione della ricerca

1. Listen for the playback seeking events from the media player, and on seek start event notification, track seeking using the `SeekStart` event:

   ```java
   public void onSeekStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
   }
   ```

1. On seek complete notification from the media player, track the end of seeking using the `SeekComplete` event:

   ```java
   public void onSeekComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
   }
   ```

See the tracking scenario [VOD playback with seeking in the main content](/help/sdk-implement/tracking-scenarios/vod-seeking.md) for more information.
