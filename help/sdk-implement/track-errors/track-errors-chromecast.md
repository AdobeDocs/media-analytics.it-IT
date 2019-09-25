---
seo-title: Tenere traccia degli errori in Chromecast
title: Tenere traccia degli errori in Chromecast
uuid: efa9de8d-c626-4cb6-b46d-108495dd013a
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tenere traccia degli errori in Chromecast{#track-errors-on-chromecast}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Implementazione del tracciamento degli errori

1. Tracciare gli errori del lettore multimediale: [trackError](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackError)

   ```
   trackError(errorId)
   ```

>[!NOTE]
>
>Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento del supporto. Se l’errore del lettore multimediale impedisce il proseguimento della riproduzione, accertatevi che la sessione di tracciamento dei contenuti multimediali sia chiusa chiamando `trackSessionEnd` dopo la chiamata `trackError`.

