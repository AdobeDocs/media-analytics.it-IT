---
title: Monitoraggio della qualità dell'esperienza su Chromecast
description: In questo argomento viene descritta l’implementazione del tracciamento della qualità dell’esperienza (QoE, QoS) tramite Media SDK on Chromecast.
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Monitoraggio della qualità dell'esperienza su Chromecast{#track-quality-of-experience-on-chromecast}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Panoramica {#overview}

Il monitoraggio della qualità dell'esperienza include la qualità del servizio (QoS) e il monitoraggio degli errori, entrambi elementi facoltativi e **non** sono richiesti per le implementazioni di tracciamento dei supporti di base. Potete utilizzare l'API Media Player per identificare le variabili relative ai QoS e al tracciamento degli errori.

## Eventi del lettore {#player-events}

### Su tutti gli eventi di modifica del bitrate

* Creare/aggiornare l'istanza dell'oggetto QoS per la riproduzione, `qosObject`
* Chiamata `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Errori del lettore

Chiamata `trackError(“media error id”);`

## Implementate {#implement}

1. Identificare quando il bitrate cambia durante la riproduzione del contenuto multimediale e creare l’ `MediaObject` istanza utilizzando le informazioni QoS.

   **Variabili QoSObject:**

   >[!TIP]
   >
   >Queste variabili sono necessarie solo se si prevede di tenere traccia dei QoS.

   | Variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `bitrate` | Bitrate corrente | Sì |
   | `startupTime` | Tempo di avvio | Sì |
   | `fps` | Valore FPS | Sì |
   | `droppedFrames` | Numero di fotogrammi saltati | Sì |

   **** Creazione di oggetti QoS: [createQoSObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createQoSObject)

   ```
   qosInfo = ADBMobile.media.createQoSObject(50000, 0, 24, 10); 
   ```

1. Quando la riproduzione cambia bitrate, chiamate l’ `BitrateChange` evento nell’istanza di Media Heartbeat: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange); 
   ```

   >[!IMPORTANT]
   >
   >Aggiornare l'oggetto QoS e richiamare l'evento di modifica del bitrate su ogni modifica del bitrate. Questo fornisce i dati QoS più precisi.

1. Accertatevi che `getQoSObject()` il metodo restituisca le informazioni QoS più aggiornate.
1. Quando il lettore multimediale rileva un errore e l'evento di errore è disponibile per l'API del lettore, utilizzare `trackError()` per acquisire le informazioni sull'errore. (Consulta [Panoramica](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento del supporto. Se l’errore del lettore multimediale impedisce il proseguimento della riproduzione, accertatevi che la sessione di tracciamento dei contenuti multimediali sia chiusa chiamando `trackSessionEnd()` dopo la chiamata `trackError()`.

