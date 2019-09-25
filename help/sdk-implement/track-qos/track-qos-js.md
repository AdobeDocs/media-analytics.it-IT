---
seo-title: Monitoraggio della qualità dell'esperienza in JavaScript
title: Monitoraggio della qualità dell'esperienza in JavaScript
uuid: 3bc762a2-9706-4b62-aa91-747f461dd13d
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Monitoraggio della qualità dell'esperienza in JavaScript{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Implementazione di QOS

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

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and  
   // <droppeFrames> with the current playback QoS values.  
   var qosObject = MediaHeartbeat.createQoSObject(<bitrate>,  
                                                  <startuptime>,  
                                                  <fps>,  
                                                  <droppedFrames>); 
   ```

1. Quando la riproduzione cambia bitrate, chiamate l’ `BitrateChange` evento nell’istanza di Media Heartbeat:

   ```js
   _onBitrateChange = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
   };
   ```

   >[!IMPORTANT]
   >
   >Aggiornare l'oggetto QoS e richiamare l'evento di modifica del bitrate su ogni modifica del bitrate. Questo fornisce i dati QoS più precisi.

1. Accertatevi che `getQoSObject()` il metodo restituisca le informazioni QoS più aggiornate.
1. Quando il lettore multimediale rileva un errore e l'evento di errore è disponibile per l'API del lettore, utilizzare `trackError()` per acquisire le informazioni sull'errore. (Consulta [Panoramica](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento del supporto. Se l’errore del lettore multimediale impedisce il proseguimento della riproduzione, accertatevi che la sessione di tracciamento dei contenuti multimediali sia chiusa chiamando `trackSessionEnd()` dopo la chiamata `trackError()`.

