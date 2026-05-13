---
title: Scopri come tracciare gli annunci utilizzando JavaScript 2.x
description: Scopri come tracciare gli eventi di buffering nelle app del browser (JS).
uuid: c380cf2c-7729-4d4a-a4da-581bd94a5896
exl-id: 62c1d5b4-2717-42b3-8343-d41e895a9da3
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/uw6vM-TESRbHRcMy2hIVQYNm3GJFIaUZTTOkOHeMih4
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 126
ht-degree: 100%

---

# Tracciare il buffering utilizzando JavaScript 2.x{#track-buffering-on-javascript}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK.](/help/getting-started/download-sdks.md)

## Costanti di tracciamento del buffer

| Nome costante | Descrizione     |
|---|---|
| `BufferStart` | Costante per il tracciamento dell’evento di avvio del buffer |
| `BufferComplete` | Costante per il tracciamento dell’evento di completamento del buffer |

## Implementare il buffering

1. Ascolta gli eventi di buffering della riproduzione dal lettore multimediale e alla notifica dell’evento di inizio buffer, traccia il buffering utilizzando l’evento `BufferStart`.

   ```js
   _onBufferStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
   };
   ```

1. Alla notifica del completamento del buffering dal lettore multimediale, traccia la fine del buffering utilizzando l’evento `BufferComplete`.

   ```js
   _onBufferComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
   };
   ```

Esamina lo scenario di tracciamento [Riproduzione VOD con buffering](/help/use-cases/tracking-scenarios/vod-buffering.md) per ulteriori informazioni.
