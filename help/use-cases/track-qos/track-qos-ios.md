---
title: Scopri come tracciare la qualità dell’esperienza su iOS
description: Scopri come implementare il tracciamento Quality of Experience (QoE, QoS) utilizzando Media SDK su iOS.
uuid: cae2c142-ed39-4234-a711-765dcabc5415
exl-id: 7f01e6eb-95bd-4e3d-93d0-8a2e68323313
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/37GAel-VlcHz-jmbicc1WphVs0y7-E8UDbBInmMT9LQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 159
ht-degree: 89%

---

# Tracciare la qualità dell’esperienza su iOS{#track-quality-of-experience-on-ios}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK.](/help/getting-started/download-sdks.md)

## Implementare QOS

1. Identificare quando il bitrate cambia durante la riproduzione del contenuto multimediale e creare l’istanza `MediaObject` utilizzando le informazioni QoS.

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
1. Quando la riproduzione commuta i bitrate, esegui la chiamata di evento `BitrateChange` nell’istanza Media Heartbeat:

   ```
   - (void)onBitrateChange:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBitrateChange  
                        mediaObject:nil  
                        data:nil];
   }
   ```

   >[!IMPORTANT]
   >
   >Aggiorna l’oggetto QoS e chiama l’evento di modifica del bitrate su ogni modifica del bitrate. Questo fornisce i dati QoS più precisi.
