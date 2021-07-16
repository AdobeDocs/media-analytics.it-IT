---
title: Scopri come tenere traccia degli errori con JavaScript 2.x
description: Scopri come implementare il tracciamento degli errori utilizzando Media SDK nelle app del browser (JS).
uuid: 5a4fc5df-2677-4189-92af-5cd074847b39
exl-id: b3012bce-4b92-408e-8b7a-57ae9d52e93d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 2%

---

# Tracciare gli errori con JavaScript 2.x{#track-errors-on-javascript}

Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione in tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Implementare il tracciamento degli errori

1. Tracciare gli errori del lettore multimediale:

   ```js
   onPlayerError = function() {
       this._mediaHeartbeat.trackError("mediaErrorId");
   };
   ```

>[!NOTE]
>
>Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento dei contenuti multimediali. Se l&#39;errore del lettore multimediale impedisce il proseguimento della riproduzione, assicurati che la sessione di tracciamento dei contenuti multimediali sia chiusa chiamando `trackSessionEnd` dopo aver chiamato `trackError`.
