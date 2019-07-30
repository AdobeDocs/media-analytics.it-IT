---
seo-title: Tracciamento della qualità dell'esperienza su Roku
title: Tracciamento della qualità dell'esperienza su Roku
uuid: a 8 b 242 ab-da 3 c -4297-9 eef-f 0 b 9684 ef 56 a
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Track quality of experience on Roku{#track-quality-of-experience-on-roku}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione in tutti gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Implementazione di QOS

1. Identify when the bitrate changes during media playback, and use the `mediaUpdateQoS` API to update the QoS info on the Media SDK.

   Variabili qosobject:

   >[!TIP]
   >
   >Queste variabili sono necessarie solo se state tracciando i QOS.

   | Variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `bitrate` | Bitrate corrente | Sì |
   | `startupTime` | Ora di avvio | Sì |
   | `fps` | Valore FPS | Sì |
   | `droppedFrames` | Numero di fotogrammi rilasciati | Sì |

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

1. When playback switches bitrates, call `trackEvent(BitrateChange)` to notify the Media SDK that the Bitrate changed.

   ```
   ADBMobile().trackMediaEvent(ADBMobile().MEDIA_BITRATE_CHANGE)
   ```

   >[!NOTE]
   >
   >You need to call `updateQoSObject` with the updated bitrate value.

   <!--
    ```
    qosContextData = {}
    ADBMobile().mediaTrackEvent(MEDIA_BITRATE_CHANGE, qosInfo, qosContextData)
    ```
 
    >[!IMPORTANT]
    >
    >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.
    -->

1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (Consulta [Panoramica](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Il tracciamento degli errori del lettore multimediale non interrompe la sessione di tracciamento multimediale. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

