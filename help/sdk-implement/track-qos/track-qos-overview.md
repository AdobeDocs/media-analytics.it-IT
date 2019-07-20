---
seo-title: Panoramica
title: Panoramica
uuid: 4 d 73 c 47 f-d 0 a 4-4228-9040-d 6432311 c 9 eb
translation-type: tm+mt
source-git-commit: 654aaef5d816e75429975d04c4e81ad4d4b6f706

---


# Panoramica{#overview}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione in tutti gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. Potete utilizzare l'API del lettore multimediale per identificare le variabili correlate a qos e il tracciamento degli errori. Ecco gli elementi chiave del tracciamento della qualità dell'esperienza:

## Player events {#player-events}

### In qualsiasi modifica di metrica qos:

Create o aggiornate l'istanza dell'oggetto qos per la riproduzione. [Riferimento API qos](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### Su tutti gli eventi modifica bitrate

Chiamata `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## Implementazione di QOS

1. Identify when any of QOS metrics change during media playback, create the `MediaObject` using the QoS information, and update the new QoS information.

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

1. Make sure that `getQoSObject()` method returns the most updated QoS information.
1. When playback switches bitrates, call the `BitrateChange` event in the Media Heartbeat instance.

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

## Validate {#section_F3174831408947A893F7E8C15659E5AA}

### Modifica bitrate

On each bitrate change, a Heartbeat `bitrate_change` call will be sent.

### Errore

Durante l'errore del lettore, viene inviata una chiamata di errore Heartbeat con il valore di errore incluso.
