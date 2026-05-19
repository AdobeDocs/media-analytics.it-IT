---
title: Scopri come tracciare gli errori utilizzando JavaScript 3.x
description: Scopri come implementare il tracciamento degli errori utilizzando Media SDK nelle app del browser (JS).
exl-id: 3769fc47-fbc4-4498-9d2a-04c88cdd0e83
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Dd505O47PRpcQmSM82BIF1wXYWXxsZNNO8c97Qj9zl4
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 100
ht-degree: 100%

---

# Tracciare gli errori utilizzando JavaScript 3.x{#track-errors-on-javascript}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione precedente dell’SDK, puoi scaricare le Guide per sviluppatori qui: [Scaricare gli SDK.](/help/getting-started/download-sdks.md)

## Implementare il tracciamento degli errori

1. Tracciare gli errori del lettore multimediale:

   ```js
   onPlayerError = function() {
       tracker.trackError("errorId");
   };
   ```

>[!NOTE]
>
>Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento dei contenuti. Se l’errore del lettore multimediale impedisce il proseguimento della riproduzione, assicurati che la sessione di tracciamento dei contenuti multimediali sia chiusa con una chiamata `trackSessionEnd` dopo la chiamata `trackError`.
