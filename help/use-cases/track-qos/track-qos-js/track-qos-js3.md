---
title: Scopri come tenere traccia della qualità dell’esperienza con JavaScript 3.x
description: "Scopri come implementare il tracciamento della qualità dell’esperienza (QoE, QoS) utilizzando Media SDK nelle app del browser che utilizzano JavaScript 3x."
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 47%

---

# Tracciamento qualità dell’esperienza con JavaScript 3.x{#track-quality-of-experience-on-javascript}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione precedente dell’SDK, puoi scaricare le Guide per sviluppatori qui: [Scaricare gli SDK.](/help/getting-started/download-sdks.md)

## Implementare QOE

1. Identificare quando il bitrate cambia durante la riproduzione del contenuto multimediale e creare il `qoeObject` tramite le informazioni QoE.

   Variabili di oggetto QoEO:

   >[!TIP]
   >
   >Queste variabili sono necessarie solo se intendi tenere traccia di QoS.

   | Variabile | Tipo | Descrizione |
   | --- | --- | --- |
   | `bitrate` | numero | Bitrate corrente |
   | `startupTime` | numero | Tempo di avvio |
   | `fps` | numero | Valore FPS |
   | `droppedFrames` | numero | Numero di fotogrammi saltati |

   Creazione di oggetti QoE:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
   tracker.updateQoEObject(qoeObject);
   ```

1. Quando la riproduzione commuta i bitrate, esegui la chiamata `BitrateChange` nell’istanza Media Heartbeat:

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
   >Aggiorna l&#39;oggetto QoE e chiama l&#39;evento di modifica del bitrate su ogni modifica del bitrate. Questo fornisce i dati QoE più precisi.

1. Assicurati di chiamare `updateQoEObject()` per fornire all&#39;SDK le informazioni QoE più aggiornate.
1. Quando il lettore multimediale rileva un errore e l&#39;evento di errore è disponibile per l&#39;API del lettore, utilizza `trackError()` per acquisire le informazioni sull’errore. (Consulta [Panoramica](/help/use-cases/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento dei contenuti. Se l’errore del lettore multimediale impedisce il proseguimento della riproduzione, assicurati che la sessione di tracciamento dei contenuti multimediali sia chiusa con una chiamata `trackSessionEnd()` dopo la chiamata `trackError()`.