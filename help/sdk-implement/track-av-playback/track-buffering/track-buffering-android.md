---
seo-title: Tracciare il buffering su Android
title: Tracciare il buffering su Android
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tracciare il buffering su Android{#track-buffering-on-android}

>[!IMPORTANT]
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricate SDks.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento del buffer

| Nome costante | Descrizione     |
|---|---|
| `MediaHeartbeat.Event.BufferStart` | Costante per il tracciamento dell’evento Start del buffer |
| `MediaHeartbeat.Event.BufferComplete` | Costante per il tracciamento dell'evento Buffer Complete |

## Implementare il buffering

1. Ascoltare gli eventi del buffering di riproduzione dal lettore multimediale e, durante la notifica dell'evento di avvio del buffer, tenere traccia del buffering utilizzando l' `BufferStart` evento:

   ```java
   public void onBufferStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null); 
   }
   ```

1. Al momento della notifica completa del buffer dal lettore multimediale, tenere traccia della fine del buffering utilizzando l' `BufferComplete` evento:

   ```java
   public void onBufferComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null); 
   }
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento della riproduzione [VOD con buffering](/help/sdk-implement/tracking-scenarios/vod-buffering.md) .
