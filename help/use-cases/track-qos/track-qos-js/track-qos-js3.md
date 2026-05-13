---
title: Scopri come tracciare la qualità dell’esperienza utilizzando JavaScript 3.x
description: Scopri come implementare il tracciamento Quality of Experience (QoE, QoS) utilizzando Media SDK nelle app browser che utilizzano JavaScript 3x.
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/aR7oVHv3n2xQnrMGHowhLFCYxhRyP1vyIrlXbKHEa5A
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 227
ht-degree: 90%

---

# Tracciare la qualità dell’esperienza utilizzando JavaScript 3.x{#track-quality-of-experience-on-javascript}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione precedente dell’SDK, puoi scaricare le Guide per sviluppatori qui: [Scaricare gli SDK.](/help/getting-started/download-sdks.md)

## Implementare QOE

1. Identifica quando il bitrate cambia durante la riproduzione del contenuto multimediale e crea l’istanza `qoeObject` tramite le informazioni QoE.

   Variabili dell’oggetto QoE:

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

1. Quando la riproduzione commuta i bitrate, esegui la chiamata di evento `BitrateChange` nell’istanza Media Heartbeat:

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
   >Aggiorna l’oggetto QoE e chiama l’evento di modifica del bitrate su ogni modifica del bitrate. Questo fornisce i dati QoE più precisi.

1. Assicurati di chiamare il metodo `updateQoEObject()` per fornire all’SDK le informazioni QoE più aggiornate.
1. Quando il lettore multimediale rileva un errore e l’evento di errore è disponibile per l’API del lettore, utilizza `trackError()` per acquisire informazioni sull’errore. (Consulta [Panoramica](/help/use-cases/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento dei contenuti. Se l’errore del lettore multimediale impedisce il proseguimento della riproduzione, assicurati che la sessione di tracciamento dei contenuti multimediali sia chiusa con una chiamata `trackSessionEnd()` dopo la chiamata `trackError()`.
