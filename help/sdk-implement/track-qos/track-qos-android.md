---
title: Monitoraggio della qualità dell'esperienza su Android
description: In questo argomento viene descritta l’implementazione del tracciamento della qualità dell’esperienza (QoE, QoS) tramite Media SDK su Android.
uuid: 81ff3939-48a6-45c1-8837-dfa33490559
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Monitoraggio della qualità dell'esperienza su Android{#track-quality-of-experience-on-android}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Implementazione di QoS

1. Identificare quando il bitrate cambia durante la riproduzione del contenuto multimediale e creare l’ `MediaObject` istanza utilizzando le informazioni QoS.

   Variabili QoSObject:

   >[!TIP]
   >
   >Queste variabili sono necessarie solo se si prevede di tenere traccia dei QoS.

   | Variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `bitrate` | Bitrate corrente | Sì |
   | `startupTime` | Tempo di avvio | Sì |
   | `fps` | Valore FPS | Sì |
   | `droppedFrames` | Numero di fotogrammi saltati | Sì |

   Creazione di oggetti QoS:

   ```java
   MediaObject qosObject =  
     MediaHeartbeat.createQoSObject(<BITRATE>,  
                                    <STARTUP_TIME>,  
                                    <FPS>,  
                                    <DROPPED_FRAMES>);
   ```

1. Accertatevi che `getQoSObject()` il metodo restituisca le informazioni QoS più aggiornate.
1. Quando la riproduzione cambia bitrate, chiamate l’ `BitrateChange` evento nell’istanza di Media Heartbeat:

   ```java
   public void onBitrateChange(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, null, null); 
   } 
   ```

   >[!IMPORTANT]
   >
   >Aggiornare l'oggetto QoS e richiamare l'evento di modifica del bitrate su ogni modifica del bitrate. Questo fornisce i dati QoS più precisi.

