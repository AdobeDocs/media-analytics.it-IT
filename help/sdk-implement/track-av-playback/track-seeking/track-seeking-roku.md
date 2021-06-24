---
title: Scopri come tracciare la ricerca su Roku
description: Scopri come tenere traccia degli eventi Seek Start e Seek Complete utilizzando Media SDK su Roku.
uuid: 0572252b-397f-4aa2-b4b5-c5346b75244a
exl-id: cb0581f7-3ced-4d46-ac6a-a309a179c21e
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 2%

---

# Tracciamento ricerca su Roku{#track-seeking-on-roku}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione in tutti gli SDK 2.x. Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento ricerca

| Nome costante | Descrizione     |
|---|---|
| `SeekStart` | Costante per il tracciamento dell’evento Seek Start . |
| `SeekComplete` | Costante per il tracciamento dell’evento Seek Complete . |

## Implementare la ricerca

1. Ascoltare gli eventi di ricerca della riproduzione dal lettore multimediale e, alla ricerca della notifica dell&#39;evento di avvio, tenere traccia della ricerca utilizzando l&#39;evento `SeekStart`.

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_START, seekInfo, seekContextData)
   ```

1. Al momento della ricerca della notifica completa da parte del lettore multimediale, tieni traccia della fine della ricerca utilizzando l&#39;evento `SeekComplete` .

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_COMPLETE, seekInfo, seekContextData)
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con ricerca nel contenuto principale](/help/sdk-implement/tracking-scenarios/vod-seeking.md) .
