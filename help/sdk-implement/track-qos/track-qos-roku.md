---
title: Monitoraggio della qualità dell'esperienza su Roku
description: In questo argomento viene descritta l’implementazione del tracciamento della qualità dell’esperienza (QoE, QoS) tramite Media SDK su Roku.
uuid: a8b242ab-da3c-4297-9eef-f0b9684ef56a
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Monitoraggio della qualità dell'esperienza su Roku{#track-quality-of-experience-on-roku}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione in tutti gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Implementazione di QOS

1. Identificare quando il bitrate cambia durante la riproduzione di contenuti multimediali e utilizzare l’ `mediaUpdateQoS` API per aggiornare le informazioni QoS sull’SDK di Media.

   Variabili QoSObject:

   >[!TIP]
   >
   >Queste variabili sono necessarie solo se si esegue il tracciamento dei QoS.

   | Variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `bitrate` | Bitrate corrente | Sì |
   | `startupTime` | Tempo di avvio | Sì |
   | `fps` | Valore FPS | Sì |
   | `droppedFrames` | Numero di fotogrammi saltati | Sì |

   Ad esempio:

   ```
   bitrate = 200000
   fps = 0
   droppedFrames = 1
   startupTime = 2
   qosinfo = adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)
   
   ADBMobile().mediaUpdateQoS(qosinfo)
   ```

   <!--
    QoS object creation:
 
    ```
    qosInfo=adb_media_init_qosinfo()
    qosInfo.bitrate = 200000
    qosInfo.fps = 0
    qosInfo.droppedFrames = 1
    qosInfo.startupTime = 2
    ```
    -->

1. Quando la riproduzione cambia bitrate, richiedete `trackEvent(BitrateChange)` di notificare all’SDK multimediale la modifica del bitrate.

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_BITRATE_CHANGE)
   ```

   >[!NOTE]
   >
   >È necessario chiamare `updateQoSObject` con il valore bitrate aggiornato.

   <!--
    ```
    qosContextData = {}
    ADBMobile().mediaTrackEvent(MEDIA_BITRATE_CHANGE, qosInfo, qosContextData)
    ```
 
    >[!IMPORTANT]
    >
    >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.
    -->

1. Quando il lettore multimediale rileva un errore e l'evento di errore è disponibile per l'API del lettore, utilizzare `trackError()` per acquisire le informazioni sull'errore. (Consulta [Panoramica](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento del supporto. Se l’errore del lettore multimediale impedisce il proseguimento della riproduzione, accertatevi che la sessione di tracciamento dei contenuti multimediali sia chiusa chiamando `trackSessionEnd()` dopo la chiamata `trackError()`.

