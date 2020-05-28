---
title: Tracciare il buffering con JavaScript 3.x
description: Descrive il tracciamento degli eventi di buffering nelle app browser (JS).
translation-type: tm+mt
source-git-commit: 8235fee973623c168dbf83f43aa85f13b4e06cff
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Tracciare il buffering con JavaScript 3.x{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 3.x. Se stai implementando versioni precedenti dell’SDK, puoi scaricare le Guide per gli sviluppatori qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento del buffer

| Nome costante | Descrizione     |
|---|---|
| `BufferStart` | Costante per il tracciamento dell’evento Start del buffer |
| `BufferComplete` | Costante per il tracciamento dell&#39;evento Buffer Complete |

## Implementare il buffering

1. Ascoltare gli eventi di buffering della riproduzione dal lettore multimediale e, durante la notifica dell&#39;evento di avvio del buffer, tenere traccia del buffering utilizzando l&#39; `BufferStart` evento.

   ```js
   _onBufferStart = function() {
       tracker.trackEvent(ADB.Media.Event.BufferStart);
   };
   ```

1. Nella notifica completa del buffer dal lettore multimediale, tenere traccia della fine del buffering utilizzando l&#39; `BufferComplete` evento.

   ```js
   _onBufferComplete = function() {
       tracker.trackEvent(ADB.Media.Event.BufferComplete);
   };
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento della riproduzione [VOD con buffering](/help/sdk-implement/tracking-scenarios/vod-buffering.md) .
