---
title: Tracciare la qualità dell’esperienza
description: Panoramica della qualità del tracciamento dell’esperienza (QoE, QoS) tramite Media SDK.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Cc5T13Z1S15MyG-CxpxMoHX-ckULmIe0dfUOe7650DE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 265
ht-degree: 99%

---

# Panoramica{#overview}

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
