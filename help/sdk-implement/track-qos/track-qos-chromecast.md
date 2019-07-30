---
seo-title: Tracciamento della qualità dell'esperienza su Chromecast
title: Tracciamento della qualità dell'esperienza su Chromecast
uuid: d 0 cdc 8 cd -4 db 0-45 ef -9470-1 cba 3996305 b
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Track quality of experience on Chromecast{#track-quality-of-experience-on-chromecast}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione in tutti gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Panoramica {#section_DDB8DFA47C5744AB9A04392AD5959BF7}

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. Potete utilizzare l'API del lettore multimediale per identificare le variabili correlate a qos e il tracciamento degli errori.

## Player events {#player-events}

### Su tutti gli eventi modifica bitrate

* Create/update the QoS object instance for the playback, `qosObject`
* Chiamata `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Errori del lettore

Chiamata `trackError(“media error id”);`

## Implementate {#section_3B8EBEB167624D0481E8AF4761F83047}

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   **Variabili qosobject:**

   >[!TIP]
   >
   >Queste variabili sono necessarie solo se prevedete di tenere traccia dei QOS.

   | Variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `bitrate` | Bitrate corrente | Sì |
   | `startupTime` | Ora di avvio | Sì |
   | `fps` | Valore FPS | Sì |
   | `droppedFrames` | Numero di fotogrammi rilasciati | Sì |

   **Creazione di oggetti qos:**[Createqosobject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createQoSObject)

   ```
   qosInfo = ADBMobile.media.createQoSObject(50000, 0, 24, 10); 
   ```

1. When playback switches bitrates, call the `BitrateChange` event in the Media Heartbeat instance: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange); 
   ```

   >[!IMPORTANT]
   >
   >Aggiornate l'oggetto qos e richiamate l'evento change bitrate su ogni modifica bitrate. Questo fornisce i dati qos più precisi.

1. Make sure that `getQoSObject()` method returns the most updated QoS information.
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (Consulta [Panoramica](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento multimediale. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

