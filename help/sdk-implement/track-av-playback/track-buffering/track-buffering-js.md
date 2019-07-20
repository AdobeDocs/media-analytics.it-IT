---
seo-title: Tenere traccia del buffering in javascript
title: Tenere traccia del buffering in javascript
uuid: c 380 cf 2 c -7729-4 d 4 a-a 4 da -581 bd 94 a 5896
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Track buffering on JavaScript{#track-buffering-on-javascript}

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

   ```js
   _onBufferStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
   };
   ```

1. On buffer complete notification from the media player, track the end of buffering using the `BufferComplete` event.

   ```js
   _onBufferComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
   };
   ```

See the tracking scenario [VOD playback with buffering](../../../sdk-implement/tracking-scenarios/vod-buffering.md) for more information.
