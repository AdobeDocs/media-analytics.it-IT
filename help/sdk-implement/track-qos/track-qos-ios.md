---
seo-title: Tracciare la qualità dell'esperienza su iOS
title: Tracciare la qualità dell'esperienza su iOS
uuid: cae 2 c 142-ed 39-4234-a 711-765 dcabc 5415
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Track quality of experience on iOS{#track-quality-of-experience-on-ios}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione in tutti gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

## Implementazione di QOS

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   Variabili qosobject:

   | Variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `bitrate` | Bitrate corrente | Sì |
   | `startupTime` | Ora di avvio | Sì |
   | `fps` | Valore FPS | Sì |
   | `droppedFrames` | Numero di fotogrammi rilasciati | Sì |

   >[!TIP]
   >
   >Queste variabili sono necessarie solo se prevedete di tenere traccia dei QOS.

   Creazione di oggetti qos:

   ```
   id qosObject = [ADBMediaHeartbeat createQoSObjectWithBitrate:[BITRATE] 
                                     startupTime:[STARTUP_TIME]  
                                     fps:[FPS]  
                                     droppedFrames:[DROPPED_FRAMES]];
   ```

1. Make sure that `getQoSObject` method returns the most updated QoS information.
1. When playback switches bitrates, call the `BitrateChange` event in the Media Heartbeat instance:

   ```
   - (void)onBitrateChange:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBitrateChange  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

   >[!IMPORTANT]
   >
   >Aggiornate l'oggetto qos e richiamate l'evento change bitrate su ogni modifica bitrate. Questo fornisce i dati qos più precisi.

