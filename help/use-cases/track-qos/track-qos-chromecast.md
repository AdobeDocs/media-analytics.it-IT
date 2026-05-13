---
title: Scopri come tenere traccia della qualità dell’esperienza su Chromecast
description: Scopri come implementare il tracciamento della qualità dell’esperienza (QoE, QoS) utilizzando Media SDK su Chromecast.
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
exl-id: 04b9b888-2727-4aa6-a934-94a02c85a490
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/VR-udMMg3tOMsbxnt-f0zjkGVZNgnCON0diYrhhMuoE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 303
ht-degree: 95%

---

# Tracciare la qualità dell’esperienza in Chromecast{#track-quality-of-experience-on-chromecast}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK.](/help/getting-started/download-sdks.md)

## Panoramica {#overview}

Il monitoraggio della qualità dell’esperienza include la qualità del servizio (QoS) e il tracciamento degli errori, entrambi elementi opzionali e **non** obbligatori per le implementazioni di tracciamento dei contenuti multimediali di base. Puoi utilizzare l’API del lettore multimediale per identificare le variabili relative ai QoS e al tracciamento degli errori.

## Eventi del lettore {#player-events}

### Su tutti gli eventi di modifica del bitrate

* Crea o aggiorna l’istanza dell’oggetto QoS per la riproduzione, `qosObject`
* Effettua la chiamata `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Sugli errori del lettore

Effettua la chiamata `trackError("media error id");`

## Implementazione {#implement}

1. Identifica quando il bitrate cambia durante la riproduzione del contenuto multimediale e crea l’istanza `MediaObject` utilizzando le informazioni QoS.

   **Variabili QoSObject:**

   >[!TIP]
   >
   >Queste variabili sono necessarie solo se intendi tenere traccia di QoS.

   | Variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `bitrate` | Bitrate corrente | Sì |
   | `startupTime` | Tempo di avvio | Sì |
   | `fps` | Valore FPS | Sì |
   | `droppedFrames` | Numero di fotogrammi saltati | Sì |

   **Creazione dell’oggetto QoS:** [createQoSObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   qosInfo = ADBMobile.media.createQoSObject(50000, 0, 24, 10);
   ```

1. Quando la riproduzione commuta i bitrate, esegui la chiamata di evento `BitrateChange` nell’istanza Media Heartbeat: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
   ```

   >[!IMPORTANT]
   >
   >Aggiorna l’oggetto QoS e chiama l’evento di modifica del bitrate su ogni modifica del bitrate. Questo fornisce i dati QoS più precisi.

1. Assicurati che il metodo `getQoSObject()` restituisca le informazioni QoS più aggiornate.
1. Quando il lettore multimediale rileva un errore e l’evento di errore è disponibile per l’API del lettore, utilizza `trackError()` per acquisire informazioni sull’errore. (Consulta [Panoramica](/help/use-cases/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento dei contenuti. Se l’errore del lettore multimediale impedisce il proseguimento della riproduzione, assicurati che la sessione di tracciamento dei contenuti multimediali sia chiusa con una chiamata `trackSessionEnd()` dopo la chiamata `trackError()`.
