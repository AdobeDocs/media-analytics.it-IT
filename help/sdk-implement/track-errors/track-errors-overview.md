---
seo-title: Panoramica
title: Panoramica
uuid: d71429e6-ef8b-4ea2-8491-ff3cdbf4357f
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Panoramica{#overview}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Implementazione del tracciamento degli errori

1. Tenere traccia degli errori del lettore multimediale.

   In caso di eventi di errore, chiamare `trackError` con le informazioni di errore.

>[!NOTE]
>
>Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento del supporto. Se l’errore del lettore multimediale impedisce il proseguimento della riproduzione, accertatevi che la sessione di tracciamento dei contenuti multimediali sia chiusa chiamando `trackSessionEnd` dopo la chiamata `trackError`.

