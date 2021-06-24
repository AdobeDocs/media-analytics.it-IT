---
title: Scopri come tenere traccia della qualità dell’esperienza su iOS
description: '"Scopri come implementare il tracciamento della qualità dell’esperienza (QoE, QoS) utilizzando Media SDK su iOS."'
uuid: cae2c142-ed39-4234-a711-765dcabc5415
exl-id: 7f01e6eb-95bd-4e3d-93d0-8a2e68323313
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 5%

---

# Tracciamento qualità dell’esperienza su iOS{#track-quality-of-experience-on-ios}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione in tutti gli SDK 2.x. Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Implementare QOS

1. Identificare quando il bitrate cambia durante la riproduzione di contenuti multimediali e creare l&#39;istanza `MediaObject` utilizzando le informazioni QoS.

   Variabili QoSObject:

   | Variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `bitrate` | Bitrate corrente | Sì |
   | `startupTime` | Tempo di avvio | Sì |
   | `fps` | Valore FPS | Sì |
   | `droppedFrames` | Numero di fotogrammi saltati | Sì |

   >[!TIP]
   >
   >Queste variabili sono necessarie solo se intendi tenere traccia di QoS.

   Creazione di oggetti QoS:

   ```
   id qosObject = [ADBMediaHeartbeat createQoSObjectWithBitrate:[BITRATE] 
                                     startupTime:[STARTUP_TIME]  
                                     fps:[FPS]  
                                     droppedFrames:[DROPPED_FRAMES]];
   ```

1. Assicurati che il metodo `getQoSObject` restituisca le informazioni QoS più aggiornate.
1. Quando la riproduzione commuta i bit rate, chiama l&#39;evento `BitrateChange` nell&#39;istanza Media Heartbeat:

   ```
   - (void)onBitrateChange:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBitrateChange  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

   >[!IMPORTANT]
   >
   >Aggiorna l&#39;oggetto QoS e chiama l&#39;evento di modifica del bitrate su ogni modifica del bitrate. Questo fornisce i dati QoS più precisi.
