---
title: Tenere traccia degli errori utilizzando JavaScript 2.x
description: In questo argomento viene descritta l’implementazione del tracciamento degli errori tramite Media SDK nelle app browser (JS).
uuid: 5a4fc5df-2677-4189-92af-5cd074847b39
translation-type: tm+mt
source-git-commit: 5f274452b9ff5770908f7e2e450935be572a22ea
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# Tenere traccia degli errori utilizzando JavaScript 2.x{#track-errors-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Implementazione del tracciamento degli errori

1. Tracciare gli errori del lettore multimediale:

   ```js
   onPlayerError = function() {
       this._mediaHeartbeat.trackError("mediaErrorId");
   };
   ```

>[!NOTE]
>
>Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento del supporto. Se l’errore del lettore multimediale impedisce il proseguimento della riproduzione, accertatevi che la sessione di tracciamento dei contenuti multimediali sia chiusa chiamando `trackSessionEnd` dopo la chiamata `trackError`.
