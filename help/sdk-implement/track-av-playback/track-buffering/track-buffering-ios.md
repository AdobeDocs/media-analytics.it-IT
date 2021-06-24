---
title: Scopri come tenere traccia del buffering su iOS
description: Scopri come tenere traccia degli eventi di buffering su iOS.
uuid: 4f4db23a-489b-4b41-bb6e-393ec64d52a2
exl-id: 5f0a3c4b-7c9e-499d-98d0-6fcf316c4d9c
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 2%

---

# Tracciamento buffering su iOS{#track-buffering-on-ios}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione in tutti gli SDK 2.x. Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento del buffer


| Nome costante | Descrizione     |
|---|---|
| `ADBMediaHeartbeatEventBufferStart` | Costante per il tracciamento dell’evento Buffer Start |
| `ADBMediaHeartbeatEventBufferComplete` | Costante per il tracciamento dell’evento Buffer Complete |

## Implementare il buffering

1. Ascoltare gli eventi di buffering di riproduzione dal lettore multimediale e nella notifica dell&#39;evento di avvio del buffer, tenere traccia del buffering utilizzando l&#39;evento `BufferStart`:

   ```
   - (void)onBufferStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Al momento della notifica completa del buffer da parte del lettore multimediale, tieni traccia della fine del buffering utilizzando l&#39;evento `BufferComplete` :

   ```
   - (void)onBufferComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con buffering](/help/sdk-implement/tracking-scenarios/vod-buffering.md) .
