---
title: Scopri come Tracciare la ricerca in Roku
description: Scopri come tenere traccia degli eventi di inizio e di completamento della ricerca utilizzando Media SDK su Roku.
uuid: 0572252b-397f-4aa2-b4b5-c5346b75244a
exl-id: cb0581f7-3ced-4d46-ac6a-a309a179c21e
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/LiR3Z-tC5yV2XcOwKTcIlcOsxx7UpBTMbn3LPXndxB4
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 133
ht-degree: 100%

---

# Tracciare la ricerca in Roku{#track-seeking-on-roku}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK.](/help/getting-started/download-sdks.md)

## Costanti di tracciamento della ricerca

| Nome costante | Descrizione     |
|---|---|
| `SeekStart` | Costante per il tracciamento dell’evento di inizio ricerca |
| `SeekComplete` | Costante per il tracciamento dell’evento di completamento della ricerca |

## Implementare la ricerca

1. Ascolta gli eventi di ricerca della riproduzione dal lettore multimediale e alla notifica dell’evento di inizio della ricerca, traccia la ricerca utilizzando l’evento `SeekStart`.

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_START, seekInfo, seekContextData)
   ```

1. Alla notifica del completamento della ricerca dal lettore multimediale, traccia la fine della ricerca utilizzando l’evento `SeekComplete`.

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_COMPLETE, seekInfo, seekContextData)
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con ricerca nel contenuto principale](/help/use-cases/tracking-scenarios/vod-seeking.md).
