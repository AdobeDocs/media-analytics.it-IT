---
title: Scopri come tenere traccia del buffering su Android
description: Scopri come tenere traccia degli eventi di buffering su Android.
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
exl-id: fcea2ef8-53c5-41fb-8b70-06599c2d9cbf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 2%

---

# Tracciamento buffering su Android{#track-buffering-on-android}

>[!IMPORTANT]
>Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione in tutti gli SDK 2.x. Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDks.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento del buffer

| Nome costante | Descrizione     |
|---|---|
| `MediaHeartbeat.Event.BufferStart` | Costante per il tracciamento dell’evento Buffer Start |
| `MediaHeartbeat.Event.BufferComplete` | Costante per il tracciamento dell’evento Buffer Complete |

## Implementare il buffering

1. Ascoltare gli eventi di buffering di riproduzione dal lettore multimediale e nella notifica dell&#39;evento di avvio del buffer, tenere traccia del buffering utilizzando l&#39;evento `BufferStart`:

   ```java
   public void onBufferStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null); 
   }
   ```

1. Al momento della notifica completa del buffer da parte del lettore multimediale, tieni traccia della fine del buffering utilizzando l&#39;evento `BufferComplete` :

   ```java
   public void onBufferComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null); 
   }
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con buffering](/help/sdk-implement/tracking-scenarios/vod-buffering.md) .
