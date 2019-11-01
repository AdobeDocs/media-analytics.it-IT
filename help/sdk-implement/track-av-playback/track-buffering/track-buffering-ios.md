---
title: Tracciare il buffering su iOS
description: Descrive il tracciamento degli eventi di buffering su iOS.
uuid: 4f4db23a-489b-4b41-bb6e-393ec64d52a2
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Tracciare il buffering su iOS{#track-buffering-on-ios}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento del buffer


| Nome costante | Descrizione     |
|---|---|
| `ADBMediaHeartbeatEventBufferStart` | Costante per il tracciamento dell’evento Start del buffer |
| `ADBMediaHeartbeatEventBufferComplete` | Costante per il tracciamento dell'evento Buffer Complete |

## Implementare il buffering

1. Ascoltare gli eventi del buffering di riproduzione dal lettore multimediale e, durante la notifica dell'evento di avvio del buffer, tenere traccia del buffering utilizzando l' `BufferStart` evento:

   ```
   - (void)onBufferStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Al momento della notifica completa del buffer dal lettore multimediale, tenere traccia della fine del buffering utilizzando l' `BufferComplete` evento:

   ```
   - (void)onBufferComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento della riproduzione [VOD con buffering](/help/sdk-implement/tracking-scenarios/vod-buffering.md) .
