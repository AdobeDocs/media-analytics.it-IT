---
title: Tracciare il buffering con JavaScript 2.x
description: Descrive il tracciamento degli eventi di buffering nelle app browser (JS).
uuid: c380cf2c-7729-4d4a-a4da-581bd94a5896
translation-type: tm+mt
source-git-commit: 8235fee973623c168dbf83f43aa85f13b4e06cff
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# Tracciare il buffering con JavaScript 2.x{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento del buffer

| Nome costante | Descrizione     |
|---|---|
| `BufferStart` | Costante per il tracciamento dell’evento Start del buffer |
| `BufferComplete` | Costante per il tracciamento dell&#39;evento Buffer Complete |

## Implementare il buffering

1. Ascoltare gli eventi di buffering della riproduzione dal lettore multimediale e, durante la notifica dell&#39;evento di avvio del buffer, tenere traccia del buffering utilizzando l&#39; `BufferStart` evento.

   ```js
   _onBufferStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
   };
   ```

1. Nella notifica completa del buffer dal lettore multimediale, tenere traccia della fine del buffering utilizzando l&#39; `BufferComplete` evento.

   ```js
   _onBufferComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
   };
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento della riproduzione [VOD con buffering](/help/sdk-implement/tracking-scenarios/vod-buffering.md) .
