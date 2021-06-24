---
title: Scopri come tenere traccia della ricerca su iOS
description: Scopri come tenere traccia degli eventi Seek Start e Seek Complete utilizzando Media SDK su iOS.
uuid: 1d31ae99-384f-4b4d-b557-4018db177349
exl-id: e8cb4962-2a14-4bfe-9a25-2405e503ba0b
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 2%

---

# Tracciamento ricerca su iOS{#track-seeking-on-ios}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione in tutti gli SDK 2.x. Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento ricerca

| Nome costante | Descrizione     |
|---|---|
| `ADBMediaHeartbeatEventSeekStart` | Costante per il tracciamento dell’evento Seek Start . |
| `ADBMediaHeartbeatEventSeekComplete` | Costante per il tracciamento dell’evento Seek Complete . |

## Implementare la ricerca

1. Ascoltare gli eventi di ricerca della riproduzione dal lettore multimediale e, alla ricerca della notifica dell&#39;evento di avvio, tenere traccia della ricerca utilizzando l&#39;evento `SeekStart`:

   ```
   - (void)onSeekStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Al momento della ricerca della notifica completa dal lettore multimediale, tieni traccia della fine della ricerca utilizzando l&#39;evento `SeekComplete` :

   ```
   - (void)onSeekComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con ricerca nel contenuto principale](/help/sdk-implement/tracking-scenarios/vod-seeking.md) .
