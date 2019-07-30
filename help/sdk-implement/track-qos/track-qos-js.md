---
seo-title: Tracciamento della qualità dell'esperienza in javascript
title: Tracciamento della qualità dell'esperienza in javascript
uuid: 3 bc 762 a 2-9706-4 b 62-aa 91-747 f 461 dd 13 d
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Track quality of experience on JavaScript{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione in tutti gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Implementazione di QOS

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   Variabili qosobject:

   >[!TIP]
   >
   >Queste variabili sono necessarie solo se prevedete di tenere traccia dei QOS.

   | Variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `bitrate` | Bitrate corrente | Sì |
   | `startupTime` | Ora di avvio | Sì |
   | `fps` | Valore FPS | Sì |
   | `droppedFrames` | Numero di fotogrammi rilasciati | Sì |

   Creazione di oggetti qos:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and  
   // <droppeFrames> with the current playback QoS values.  
   var qosObject = MediaHeartbeat.createQoSObject(<bitrate>,  
                                                  <startuptime>,  
                                                  <fps>,  
                                                  <droppedFrames>); 
   ```

1. When playback switches bitrates, call the `BitrateChange` event in the Media Heartbeat instance:

   ```js
   _onBitrateChange = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
   };
   ```

   >[!IMPORTANT]
   >
   >Aggiornate l'oggetto qos e richiamate l'evento change bitrate su ogni modifica bitrate. Questo fornisce i dati qos più precisi.

1. Make sure that `getQoSObject()` method returns the most updated QoS information.
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (Consulta [Panoramica](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento multimediale. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

