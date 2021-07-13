---
title: Scopri come tenere traccia del buffering con JavaScript 3.x
description: Scopri come tenere traccia degli eventi di buffering nelle app del browser (JS).
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 2%

---

# Tracciamento buffering con JavaScript 3.x{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione in tutti gli SDK 3.x. Se implementi una versione precedente dell’SDK, puoi scaricare le Guide per sviluppatori qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento del buffer

| Nome costante | Descrizione     |
|---|---|
| `BufferStart` | Costante per il tracciamento dell’evento Buffer Start |
| `BufferComplete` | Costante per il tracciamento dell’evento Buffer Complete |

## Implementare il buffering

1. Ascolta gli eventi di buffering di riproduzione dal lettore multimediale e, in caso di notifica dell&#39;evento di avvio del buffer, tieni traccia del buffering utilizzando l&#39;evento `BufferStart` .

   ```js
   _onBufferStart = function() {
       tracker.trackEvent(ADB.Media.Event.BufferStart);
   };
   ```

1. Al momento della notifica completa del buffer da parte del lettore multimediale, tieni traccia della fine del buffering utilizzando l&#39;evento `BufferComplete` .

   ```js
   _onBufferComplete = function() {
       tracker.trackEvent(ADB.Media.Event.BufferComplete);
   };
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con buffering](/help/sdk-implement/tracking-scenarios/vod-buffering.md) .
