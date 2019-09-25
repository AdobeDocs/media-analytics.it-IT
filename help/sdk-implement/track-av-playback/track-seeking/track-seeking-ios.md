---
seo-title: Tracciare la ricerca su iOS
title: Tracciare la ricerca su iOS
uuid: 1d31ae99-384f-4b4d-b557-4018db177349
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tracciare la ricerca su iOS{#track-seeking-on-ios}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento delle ricerche

| Nome costante | Descrizione     |
|---|---|
| `ADBMediaHeartbeatEventSeekStart` | Costante per il tracciamento dell'evento Seek Start. |
| `ADBMediaHeartbeatEventSeekComplete` | Costante per il tracciamento dell'evento Seek Complete. |

## Implementa ricerca

1. Ascoltare gli eventi di ricerca della riproduzione dal lettore multimediale e, durante la ricerca, avviare la notifica dell’evento, tenere traccia della ricerca mediante l’ `SeekStart` evento:

   ```
   - (void)onSeekStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Alla ricerca della notifica completa dal lettore multimediale, tenete traccia della fine della ricerca mediante l’ `SeekComplete` evento:

   ```
   - (void)onSeekComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

Per ulteriori informazioni, vedi la riproduzione [VOD dello scenario di tracciamento con la ricerca nel contenuto](/help/sdk-implement/tracking-scenarios/vod-seeking.md) principale.
