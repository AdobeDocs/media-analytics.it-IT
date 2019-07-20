---
seo-title: Tracciamento della qualità dell'esperienza su Android
title: Tracciamento della qualità dell'esperienza su Android
uuid: 81 ff 3939-48 a 6-45 c 1-8837-ddfa 33490559
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Track quality of experience on Android{#track-quality-of-experience-on-android}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione in tutti gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

## Informazioni su qos

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

   ```java
   MediaObject qosObject =  
     MediaHeartbeat.createQoSObject(<BITRATE>,  
                                    <STARTUP_TIME>,  
                                    <FPS>,  
                                    <DROPPED_FRAMES>);
   ```

1. Make sure that `getQoSObject()` method returns the most updated QoS information.
1. When playback switches bitrates, call the `BitrateChange` event in the Media Heartbeat instance:

   ```java
   public void onBitrateChange(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, null, null); 
   } 
   ```

   >[!IMPORTANT]
   >
   >Aggiornate l'oggetto qos e richiamate l'evento change bitrate su ogni modifica bitrate. Questo fornisce i dati qos più precisi.

