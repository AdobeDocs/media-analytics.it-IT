---
title: Scopri come tracciare la ricerca utilizzando JavaScript 2.x
description: Scopri come tracciare gli eventi di inizio e di completamento della ricerca utilizzando il Media SDK nelle app del browser (JS 2.x).
uuid: 089947fb-8bae-4ae8-b215-53793620efd7
exl-id: 90f35376-24d8-405d-82b4-d6b737acf7b9
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/wQkUvm0BhqYGd9q-k2YKe2f0kkhjkM3hpwDYuAIw3QU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 141
ht-degree: 100%

---

# Tracciare la ricerca utilizzando JavaScript 2.x{#track-seeking-on-javascript}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK.](/help/getting-started/download-sdks.md)

## Costanti di tracciamento della ricerca

| Nome costante | Descrizione     |
|---|---|
| `SeekStart` | Costante per il tracciamento dell’evento di inizio ricerca |
| `SeekComplete` | Costante per il tracciamento dell’evento di completamento della ricerca |

## Implementare la ricerca

1. Ascolta gli eventi di ricerca della riproduzione dal lettore multimediale e alla notifica dell’evento di inizio della ricerca, traccia la ricerca utilizzando l’evento `SeekStart`:

   ```js
   _onSeekStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
   };
   ```

1. Alla notifica del completamento della ricerca dal lettore multimediale, traccia la fine della ricerca utilizzando l’evento `SeekComplete`:

   ```js
   _onSeekComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
   };
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con ricerca nel contenuto principale](/help/use-cases/tracking-scenarios/vod-seeking.md).
