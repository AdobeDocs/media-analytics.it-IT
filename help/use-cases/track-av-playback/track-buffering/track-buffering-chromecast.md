---
title: Scopri come tracciare il buffering in Chromecast
description: Scopri come tracciare gli eventi di buffering in Chromecast.
uuid: f6fa3a1a-d7de-4293-bd11-ebe9e130badd
exl-id: 26fd1e2a-4103-486f-be12-36b088d28cb6
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/zIbnO6-BkK6uxr7-wdIzog76FsVtqFatq-RFu-PjHiI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 142
ht-degree: 100%

---

# Tracciare il buffering in Chromecast{#track-buffering-on-chromecast}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK.](/help/getting-started/download-sdks.md)

## Costanti di tracciamento del buffer


| Nome costante | Descrizione     |
|---|---|
| `BufferStart` | Costante per il tracciamento dell’evento di avvio del buffer |
| `BufferComplete` | Costante per il tracciamento dell’evento di completamento del buffer |

## Implementare il buffering

1. Ascolta gli eventi di buffering di riproduzione dal lettore multimediale e alla notifica dell’evento di avvio del buffer, tieni traccia del buffering utilizzando l’evento `BufferStart`: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);
   ```

1. Al momento della notifica di completamento del buffer da parte del lettore multimediale, tieni traccia della termine del buffering utilizzando l’evento `BufferComplete`: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
   ```

Esamina lo scenario di tracciamento [Riproduzione VOD con buffering](/help/use-cases/tracking-scenarios/vod-buffering.md) per ulteriori informazioni.
