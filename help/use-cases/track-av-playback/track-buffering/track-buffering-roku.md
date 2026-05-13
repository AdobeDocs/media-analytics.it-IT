---
title: Scopri come tenere traccia del buffering su Roku
description: Scopri come tenere traccia degli eventi di buffering su Roku.
uuid: 6666b270-9aa3-42ff-95a8-f12502022d47
exl-id: 73b10b42-02ab-47f8-8250-58f03c5e0dd1
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/YXeUkgBa7rjDXRYXsB4l0-vr-edBefGbehqTOpbZcrE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 100%

---

# Tracciare il buffering in Roku{#track-buffering-on-roku}

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

1. Ascolta gli eventi di buffering della riproduzione dal lettore multimediale e alla notifica dell’evento di inizio buffer, traccia il buffering utilizzando l’evento `BufferStart`.

   ```
   bufferInfo = {}
   bufferContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_BUFFER_START, bufferInfo, bufferContextData)
   ```

1. Alla notifica del completamento del buffering dal lettore multimediale, traccia la fine del buffering utilizzando l’evento `BufferComplete`.

   ```
   bufferInfo = {}
   bufferContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_BUFFER_COMPLETE, bufferInfo, bufferContextData)
   ```

Esamina lo scenario di tracciamento [Riproduzione VOD con buffering](/help/use-cases/tracking-scenarios/vod-buffering.md) per ulteriori informazioni.
