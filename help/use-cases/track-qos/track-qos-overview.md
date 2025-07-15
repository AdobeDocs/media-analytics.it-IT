---
title: Tracciare la qualità dell’esperienza
description: Panoramica della qualità del tracciamento dell’esperienza (QoE, QoS) tramite Media SDK.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 99%

---

# Panoramica {#overview}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK.](/help/getting-started/download-sdks.md)

Il monitoraggio della qualità dell’esperienza include la qualità del servizio (QoS) e il tracciamento degli errori, entrambi elementi opzionali e **non** obbligatori per le implementazioni di tracciamento dei contenuti multimediali di base. Puoi utilizzare l’API del lettore multimediale per identificare le variabili relative ai QoS e al tracciamento degli errori. Di seguito sono riportati gli elementi chiave per il tracciamento della qualità dell’esperienza:

## Eventi del lettore {#player-events}

### Su qualsiasi modifica della metrica QoS:

Crea o aggiorna l’istanza dell’oggetto QoS per la riproduzione. [Riferimento API QoS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### Su tutti gli eventi di modifica del bitrate

Chiamata `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## Implementare QOS

1. Identifica quando una qualsiasi delle metriche QoS cambia durante la riproduzione di contenuti multimediali, crea `MediaObject` utilizzando le informazioni QoS e aggiornando queste ultime con i nuovi dati.

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

1. Assicurati che il metodo `getQoSObject()` restituisca le informazioni QoS più aggiornate.
1. Quando la riproduzione commuta i bitrate, esegui la chiamata `BitrateChange` nell’istanza Media Heartbeat.

   >[!IMPORTANT]
   >
   >Aggiorna l’oggetto QoS e chiama l’evento di modifica del bitrate su ogni modifica del bitrate. Questo fornisce i dati QoS più precisi.

Il codice di esempio seguente utilizza l’SDK JavaScript 2.x per un lettore multimediale HTML5. Usa questo codice con il codice di riproduzione del contenuto multimediale principale.

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
