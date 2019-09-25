---
seo-title: Tracciare il buffering su JavaScript
title: Tracciare il buffering su JavaScript
uuid: c380cf2c-7729-4d4a-a4da-581bd94a5896
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tracciare il buffering su JavaScript{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento del buffer

| Nome costante | Descrizione     |
|---|---|
| `BufferStart` | Costante per il tracciamento dell’evento Start del buffer |
| `BufferComplete` | Costante per il tracciamento dell'evento Buffer Complete |

## Implementare il buffering

1. Ascoltare gli eventi di buffering della riproduzione dal lettore multimediale e, durante la notifica dell'evento di avvio del buffer, tenere traccia del buffering utilizzando l' `BufferStart` evento.

   ```js
   _onBufferStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
   };
   ```

1. Nella notifica completa del buffer dal lettore multimediale, tenere traccia della fine del buffering utilizzando l' `BufferComplete` evento.

   ```js
   _onBufferComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
   };
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento della riproduzione [VOD con buffering](/help/sdk-implement/tracking-scenarios/vod-buffering.md) .
