---
title: Tenere traccia degli errori utilizzando JavaScript 3.x
description: In questo argomento viene descritta l’implementazione del tracciamento degli errori tramite Media SDK nelle app browser (JS).
translation-type: tm+mt
source-git-commit: fa161e2d41629fdfe77100d87d6a44728e23d77f
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Tenere traccia degli errori utilizzando JavaScript 3.x{#track-errors-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 3.x. Se stai implementando versioni precedenti dell’SDK, puoi scaricare le Guide per gli sviluppatori qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Implementazione del tracciamento degli errori

1. Tracciare gli errori del lettore multimediale:

   ```js
   onPlayerError = function() {
       tracker.trackError("errorId");
   };
   ```

>[!NOTE]
>
>Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento del supporto. Se l’errore del lettore multimediale impedisce il proseguimento della riproduzione, accertatevi che la sessione di tracciamento dei contenuti multimediali sia chiusa chiamando `trackSessionEnd` dopo la chiamata `trackError`.
