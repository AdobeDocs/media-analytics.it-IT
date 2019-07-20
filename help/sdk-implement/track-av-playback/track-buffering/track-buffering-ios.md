---
seo-title: Tenere traccia del buffering su iOS
title: Tenere traccia del buffering su iOS
uuid: 4 f 4 db 23 a -489 b -4 b 41-bb 6 e -393 ec 64 d 52 a 2
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Track buffering on iOS{#track-buffering-on-ios}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione in tutti gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../../sdk-implement/download-sdks.md)

## Costanti di tracciamento del buffer


| Nome costante | Descrizione     |
|---|---|
| `ADBMediaHeartbeatEventBufferStart` | Costante per il tracciamento dell'evento di inizio del buffer |
| `ADBMediaHeartbeatEventBufferComplete` | Costante per il tracciamento dell'evento di completamento buffer |

## Implementare il buffering

1. Listen for the playback buffering events from media player, and on buffer start event notification, track buffering using the `BufferStart` event:

   ```
   - (void)onBufferStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. On buffer complete notification from the media player, track the end of buffering using the `BufferComplete` event:

   ```
   - (void)onBufferComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

See the tracking scenario [VOD playback with buffering](../../../sdk-implement/tracking-scenarios/vod-buffering.md) for more information.
