---
title: Tracciare il buffering su Chromecast
description: Descrive il tracciamento degli eventi buffering su Chromecast.
uuid: f6fa3a1a-d7de-4293-bd11-ebe9e130badd
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Tracciare il buffering su Chromecast{#track-buffering-on-chromecast}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento del buffer


| Nome costante | Descrizione     |
|---|---|
| `BufferStart` | Costante per il tracciamento dell’evento Start del buffer |
| `BufferComplete` | Costante per il tracciamento dell'evento Buffer Complete |

## Implementare il buffering

1. Ascoltare gli eventi del buffering di riproduzione dal lettore multimediale e, durante la notifica dell'evento di avvio del buffer, tenere traccia del buffering utilizzando l' `BufferStart` evento: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);
   ```

1. Al momento della notifica completa del buffer dal lettore multimediale, tenere traccia della fine del buffering utilizzando l' `BufferComplete` evento: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento della riproduzione [VOD con buffering](/help/sdk-implement/tracking-scenarios/vod-buffering.md) .
