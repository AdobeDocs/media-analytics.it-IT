---
title: Scopri come tenere traccia del buffering con JavaScript 2.x
description: Scopri come tenere traccia degli eventi di buffering nelle app del browser (JS).
uuid: c380cf2c-7729-4d4a-a4da-581bd94a5896
exl-id: 62c1d5b4-2717-42b3-8343-d41e895a9da3
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 2%

---

# Tracciamento buffering con JavaScript 2.x{#track-buffering-on-javascript}

Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione in tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento del buffer

| Nome costante | Descrizione     |
|---|---|
| `BufferStart` | Costante per il tracciamento dell’evento Buffer Start |
| `BufferComplete` | Costante per il tracciamento dell’evento Buffer Complete |

## Implementare il buffering

1. Ascolta gli eventi di buffering di riproduzione dal lettore multimediale e, in caso di notifica dell&#39;evento di avvio del buffer, tieni traccia del buffering utilizzando l&#39;evento `BufferStart` .

   ```js
   _onBufferStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
   };
   ```

1. Al momento della notifica completa del buffer da parte del lettore multimediale, tieni traccia della fine del buffering utilizzando l&#39;evento `BufferComplete` .

   ```js
   _onBufferComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
   };
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con buffering](/help/sdk-implement/tracking-scenarios/vod-buffering.md) .
