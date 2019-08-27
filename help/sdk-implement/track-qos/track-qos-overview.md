---
seo-title: Panoramica
title: Panoramica
uuid: 4 d 73 c 47 f-d 0 a 4-4228-9040-d 6432311 c 9 eb
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Panoramica{#overview}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione in tutti gli SDK 2. x. Se implementhi una versione 1. x dell'SDK, puoi scaricare le guide per sviluppatori 1. x qui: [Scarica gli SDK.](/help/sdk-implement/download-sdks.md)

La qualità del tracciamento delle esperienze include la qualità del servizio (qos) e il tracciamento degli errori, entrambi sono elementi facoltativi e **non** sono necessari per le implementazioni di tracciamento dei contenuti multimediali principali. Potete utilizzare l'API del lettore multimediale per identificare le variabili correlate a qos e il tracciamento degli errori. Ecco gli elementi chiave del tracciamento della qualità dell'esperienza:

## Eventi del lettore {#player-events}

### In qualsiasi modifica di metrica qos:

Create o aggiornate l'istanza dell'oggetto qos per la riproduzione. [Riferimento API qos](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### Su tutti gli eventi modifica bitrate

Chiamata `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## Implementazione di QOS

1. Identificate quando una delle metriche QOS cambia durante la riproduzione del file multimediale, create le `MediaObject` informazioni qos e aggiornate le nuove informazioni su qos.

   Variabili qosobject:

   >[!TIP]
   >
   >Queste variabili sono necessarie solo se prevedete di tenere traccia dei QOS.

   | Variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `bitrate` | Bitrate corrente | Sì |
   | `startupTime` | Ora di avvio | Sì |
   | `fps` | Valore FPS | Sì |
   | `droppedFrames` | Numero di fotogrammi rilasciati | Sì |

1. Accertatevi che `getQoSObject()` il metodo restituisca le informazioni qos più aggiornate.
1. Quando la riproduzione attiva bitrate, chiama l' `BitrateChange` evento nell'istanza Media Heartbeat.

   >[!IMPORTANT]
   >
   >Aggiornate l'oggetto qos e richiamate l'evento change bitrate su ogni modifica bitrate. Questo fornisce i dati qos più precisi.

Il seguente codice di esempio utilizza l'SDK javascript 2. x per un lettore multimediale HTML 5. Utilizzate questo codice con il codice di riproduzione multimediale principale.

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

