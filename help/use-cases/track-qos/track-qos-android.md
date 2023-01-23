---
title: Scopri come tracciare la qualità dell’esperienza su Android
description: “Scopri come implementare il tracciamento della qualità dell’esperienza (QoE, QoS) utilizzando Media SDK su Android”.
uuid: 81ff3939-48a6-45c1-8837-ddfa33490559
exl-id: cee8b119-bca2-4a5c-8111-2b49f7eede66
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '156'
ht-degree: 100%

---

# Tracciare la qualità dell’esperienza su Android{#track-quality-of-experience-on-android}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK.](/help/getting-started/download-sdks.md)

## Implementare QoS

1. Identificare quando il bitrate cambia durante la riproduzione del contenuto multimediale e creare l’istanza `MediaObject` utilizzando le informazioni QoS.

   Variabili QoSObject:

   >[!TIP]
   >
   >Queste variabili sono necessarie solo se intendi tenere traccia di QoS.

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

1. Assicurati che il metodo `getQoSObject()` restituisca le informazioni QoS più aggiornate.
1. Quando la riproduzione commuta i bitrate, esegui la chiamata di evento `BitrateChange` nell’istanza Media Heartbeat:

   ```java
   public void onBitrateChange(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, null, null);
   }
   ```

   >[!IMPORTANT]
   >
   >Aggiorna l’oggetto QoS e chiama l’evento di modifica del bitrate su ogni modifica del bitrate. Questo fornisce i dati QoS più precisi.
