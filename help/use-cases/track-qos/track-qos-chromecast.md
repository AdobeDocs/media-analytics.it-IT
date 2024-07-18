---
title: Scopri come tenere traccia della qualità dell’esperienza su Chromecast
description: “Scopri come implementare il tracciamento della qualità dell’esperienza (QoE, QoS) utilizzando Media SDK su Chromecast”.
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
exl-id: 04b9b888-2727-4aa6-a934-94a02c85a490
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 100%

---

# Tracciare la qualità dell’esperienza in Chromecast{#track-quality-of-experience-on-chromecast}

Le istruzioni seguenti forniscono indicazioni per l’implementazione con tutti gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK.](/help/getting-started/download-sdks.md)

## Panoramica {#overview}

Il monitoraggio della qualità dell’esperienza include la qualità del servizio (QoS) e il tracciamento degli errori, entrambi elementi opzionali e **non** obbligatori per le implementazioni di tracciamento dei contenuti multimediali di base. Per identificare le variabili relative a QoS e al tracciamento degli errori, è possibile utilizzare l’API del lettore multimediale.

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
