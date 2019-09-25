---
seo-title: Ricerca di tracce su Chromecast
title: Ricerca di tracce su Chromecast
uuid: 8018e6c4-feed9-4de7-9eae-c720da55ad8c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Ricerca di tracce su Chromecast{#track-seeking-on-chromecast}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento delle ricerche

| Nome costante | Descrizione     |
|---|---|
| `SeekStart` | Costante per il tracciamento dell'evento Seek Start. |
| `SeekComplete` | Costante per il tracciamento dell'evento Seek Complete. |

## Implementa ricerca

1. Ascoltare gli eventi di ricerca della riproduzione dal lettore multimediale e, durante la ricerca, avviare la notifica dell’evento, tenere traccia della ricerca mediante l’ `SeekStart` evento: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekStart); 
   ```

1. Alla ricerca della notifica completa dal lettore multimediale, tenete traccia della fine della ricerca mediante l’ `SeekComplete` evento: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekComplete); 
   ```

Per ulteriori informazioni, vedi la riproduzione [VOD dello scenario di tracciamento con la ricerca nel contenuto](/help/sdk-implement/tracking-scenarios/vod-seeking.md) principale.
