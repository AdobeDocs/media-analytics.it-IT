---
title: Monitoraggio della qualità dell'esperienza con JavaScript 3.x
description: Questo argomento descrive l'implementazione del tracciamento della qualità dell'esperienza (QoE, QoS) tramite Media SDK nelle app browser che utilizzano JavaScript 3x.
translation-type: tm+mt
source-git-commit: b165c9d133637fd0f1c529a98a936f8f31b72465
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 2%

---


# Monitoraggio della qualità dell&#39;esperienza con JavaScript 3.x{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 3.x. Se stai implementando versioni precedenti dell’SDK, puoi scaricare le Guide per gli sviluppatori qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Implementazione del QOE

1. Identificare quando il bitrate cambia durante la riproduzione del contenuto multimediale e creare l’ `qoeObject` istanza utilizzando le informazioni sul QoE.

   Variabili QoEbject:

   >[!TIP]
   >
   >Queste variabili sono necessarie solo se si prevede di tenere traccia dei QoS.

   | Variabile | Tipo | Descrizione |
   | --- | --- | --- |
   | `bitrate` | number | Bitrate corrente |
   | `startupTime` | number | Tempo di avvio |
   | `fps` | number | Valore FPS |
   | `droppedFrames` | number | Numero di fotogrammi saltati |

   Creazione di oggetti QoE:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
   ```

1. Quando la riproduzione cambia bitrate, chiamate l’ `BitrateChange` evento nell’istanza di Media Heartbeat:

   ```js
   _onBitrateChange = function() {
       // If the new bitrate value is available provide it to the tracker.
       var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
       tracker.updateQoEObject(qoeObject);
   
       tracker.trackEvent(ADB.Media.Event.BitrateChange);
   };
   ```

   >[!IMPORTANT]
   >
   >Aggiornate l&#39;oggetto QoE e richiamate l&#39;evento di modifica del bitrate a ogni modifica del bitrate. Questo fornisce i dati QoE più precisi.

1. Assicurati di invocare `updateQoEObject()` il metodo per fornire all’SDK le informazioni QoE più aggiornate.
1. Quando il lettore multimediale rileva un errore e l&#39;evento di errore è disponibile per l&#39;API del lettore, utilizzare `trackError()` per acquisire le informazioni sull&#39;errore. (Consulta [Panoramica](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento del supporto. Se l’errore del lettore multimediale impedisce il proseguimento della riproduzione, accertatevi che la sessione di tracciamento dei contenuti multimediali sia chiusa chiamando `trackSessionEnd()` dopo la chiamata `trackError()`.
