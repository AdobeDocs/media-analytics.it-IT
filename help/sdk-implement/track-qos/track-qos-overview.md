---
title: Panoramica
description: Panoramica della qualità del tracciamento dell’esperienza (QoE, QoS) mediante l’SDK per file multimediali.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Panoramica{#overview}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

Il monitoraggio della qualità dell'esperienza include la qualità del servizio (QoS) e il monitoraggio degli errori, entrambi elementi facoltativi e **non** sono richiesti per le implementazioni di tracciamento dei supporti di base. Potete utilizzare l'API Media Player per identificare le variabili relative ai QoS e al tracciamento degli errori. Gli elementi chiave per il monitoraggio della qualità dell'esperienza sono i seguenti:

## Eventi del lettore {#player-events}

### In caso di modifiche della metrica QoS:

Creare o aggiornare l'istanza dell'oggetto QoS per la riproduzione. [Riferimento API QoS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### Su tutti gli eventi di modifica del bitrate

Chiamata `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## Implementazione di QOS

1. Identificare il momento in cui una qualsiasi delle metriche QOS cambia durante la riproduzione multimediale, creare l' `MediaObject` oggetto utilizzando le informazioni QoS e aggiornare le nuove informazioni QoS.

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

1. Accertatevi che `getQoSObject()` il metodo restituisca le informazioni QoS più aggiornate.
1. Quando la riproduzione cambia bitrate, chiamate l’ `BitrateChange` evento nell’istanza Media Heartbeat.

   >[!IMPORTANT]
   >
   >Aggiornare l'oggetto QoS e richiamare l'evento di modifica del bitrate su ogni modifica del bitrate. Questo fornisce i dati QoS più precisi.

Il codice di esempio seguente utilizza l’SDK JavaScript 2.x per un lettore multimediale HTML5. Utilizzare questo codice con il codice di riproduzione del contenuto multimediale di base.

```js
var mediaDelegate = new MediaHeartbeatDelegate(); 
...  
 
// This is called periodically by MediaHeartbeat instance 
mediaDelegate.prototype.getQoSObject = function() { 
    return this.qosInfo; 
}; 
 
if (e.type == "qos_update") { 
    var qosInfo = MediaHeartbeat.createQoSObject(<BITRATE>,<STARTUP_TIME>,<FPS>,<DROPPED_FRAMES>); 
    mediaDelegate.qosInfo = qosInfo; 
}; 
 
if (e.type == "bitrate_change") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
};
```

