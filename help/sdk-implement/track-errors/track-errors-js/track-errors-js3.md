---
title: Scopri come tenere traccia degli errori con JavaScript 3.x
description: Scopri come implementare il tracciamento degli errori utilizzando Media SDK nelle app del browser (JS).
exl-id: 3769fc47-fbc4-4498-9d2a-04c88cdd0e83
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 2%

---

# Tracciamento errori con JavaScript 3.x{#track-errors-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione in tutti gli SDK 3.x. Se implementi una versione precedente dell’SDK, puoi scaricare le Guide per sviluppatori qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Implementare il tracciamento degli errori

1. Tracciare gli errori del lettore multimediale:

   ```js
   onPlayerError = function() {
       tracker.trackError("errorId");
   };
   ```

>[!NOTE]
>
>Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento dei contenuti multimediali. Se l&#39;errore del lettore multimediale impedisce il proseguimento della riproduzione, assicurati che la sessione di tracciamento dei contenuti multimediali sia chiusa chiamando `trackSessionEnd` dopo aver chiamato `trackError`.
