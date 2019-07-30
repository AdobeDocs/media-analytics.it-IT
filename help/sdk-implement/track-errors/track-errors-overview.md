---
seo-title: Panoramica
title: Panoramica
uuid: d 71429 e 6-ef 8 b -4 ea 2-8491-ff 3 cdbf 4357 f
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Panoramica{#overview}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione in tutti gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Implementazione del tracciamento degli errori

1. Tenere traccia degli errori del lettore multimediale.

   On error events, call `trackError` with the error information.

>[!NOTE]
>
>Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento multimediale. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

