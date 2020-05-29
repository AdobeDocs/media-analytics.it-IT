---
title: Monitoraggio della qualità dell'esperienza con JavaScript 2.x
description: Questo argomento descrive l'implementazione del tracciamento della qualità dell'esperienza (QoE, QoS) tramite Media SDK nelle app browser che utilizzano JavaScript 2.x.
uuid: 3bc762a2-9706-4b62-aa91-747f461dd13d
translation-type: tm+mt
source-git-commit: fa161e2d41629fdfe77100d87d6a44728e23d77f
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 4%

---


# Monitoraggio della qualità dell&#39;esperienza con JavaScript 2.x{#track-quality-of-experience-on-javascript}

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
   >Aggiornare l&#39;oggetto QoS e richiamare l&#39;evento di modifica del bitrate su ogni modifica del bitrate. Questo fornisce i dati QoS più precisi.

1. Accertatevi che `getQoSObject()` il metodo restituisca le informazioni QoS più aggiornate.
1. Quando il lettore multimediale rileva un errore e l&#39;evento di errore è disponibile per l&#39;API del lettore, utilizzare `trackError()` per acquisire le informazioni sull&#39;errore. (Consulta [Panoramica](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento del supporto. Se l’errore del lettore multimediale impedisce il proseguimento della riproduzione, accertatevi che la sessione di tracciamento dei contenuti multimediali sia chiusa chiamando `trackSessionEnd()` dopo la chiamata `trackError()`.
