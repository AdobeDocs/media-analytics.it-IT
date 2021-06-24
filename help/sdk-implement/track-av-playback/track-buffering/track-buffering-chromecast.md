---
title: Scopri come tenere traccia del buffering in Chromecast
description: Scopri come tenere traccia degli eventi di buffering in Chromecast.
uuid: f6fa3a1a-d7de-4293-bd11-ebe9e130badd
exl-id: 26fd1e2a-4103-486f-be12-36b088d28cb6
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 2%

---

# Tracciamento buffering in Chromecast{#track-buffering-on-chromecast}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione in tutti gli SDK 2.x. Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento del buffer


| Nome costante | Descrizione     |
|---|---|
| `BufferStart` | Costante per il tracciamento dell’evento Buffer Start |
| `BufferComplete` | Costante per il tracciamento dell’evento Buffer Complete |

## Implementare il buffering

1. Ascoltare gli eventi di buffering di riproduzione dal lettore multimediale e nella notifica dell&#39;evento di avvio del buffer, tenere traccia del buffering utilizzando l&#39;evento `BufferStart`: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);
   ```

1. Al momento della notifica completa del buffer da parte del lettore multimediale, tieni traccia della fine del buffering utilizzando l&#39;evento `BufferComplete` : [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con buffering](/help/sdk-implement/tracking-scenarios/vod-buffering.md) .
