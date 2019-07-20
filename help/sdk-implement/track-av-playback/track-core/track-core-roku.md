---
seo-title: Tracciare la riproduzione di base su Roku
title: Tracciare la riproduzione di base su Roku
uuid: a 8 aa 7 b 3 c -2 d 39-44 d 7-8 ebc-b 101 d 130101 f
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Track core playback on Roku{#track-core-playback-on-roku}

>[!IMPORTANT]
>Questa documentazione copre il tracciamento nella versione 2. x dell'SDK. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [Download SDKs](../../../sdk-implement/download-sdks.md)

1. **Configurazione di tracciamento iniziale**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   **`MediaObject`riferimento:**

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome video | Sì |
   | `mediaid` | Identificatore univoco video | Sì |
   | `length` | Lunghezza video | Sì |
   | `streamType` | Stream type (see _StreamType constants_ below) | Sì |
   | `mediaType` | Media type (see _MediaType constants_ below) | Sì |

   **`StreamType`costanti:**

   | Nome costante | Descrizione   |
   |---|---|
   | `MEDIA_STREAM_TYPE_VOD` | Tipo di flusso per Video su richiesta. |
   | `MEDIA_STREAM_TYPE_LIVE` | Tipo di flusso per il contenuto LIVE. |
   | `MEDIA_STREAM_TYPE_LINEAR` | Tipo di flusso per il contenuto lineare. |
   | `MEDIA_STREAM_TYPE_AOD` | Tipo di flusso per Audio on demand |
   | `MEDIA_STREAM_TYPE_AUDIOBOOK` | Tipo di flusso per il libro audio |
   | `MEDIA_STREAM_TYPE_PODCAST` | Tipo di flusso per Podcast |

   **`MediaType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `MEDIA_STREAM_TYPE_AUDIO` | Tipo di file multimediale per i flussi audio. |
   | `MEDIA_STREAM_TYPE_VIDEO` | Tipo di supporto per i flussi video. |

   **Create un oggetto info per file multimediali per video con contenuto VOD:**

   ```
    mediaInfo = adb_media_init_mediainfo(
     "<MEDIA_NAME>",
     "<MEDIA_ID>",
     600,
     ADBMobile().MEDIA_STREAM_TYPE_VOD,
     ADBMobile().MEDIA_TYPE_VIDEO
   )
   ```

    oppure 

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_VOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_VIDEO
   ```

   **Create un oggetto info per file multimediali per video con contenuto AOD:**

   ```
   mediaInfo = adb_media_init_mediainfo(
    "<MEDIA_NAME>", 
    "<MEDIA_ID>", 
    600, 
    ADBMobile().MEDIA_STREAM_TYPE_AOD, 
    ADBMobile().MEDIA_TYPE_AUDIO
   )
   ```

    oppure 

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_AOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_AUDIO
   ```

1. **Allega metadati**

   Allega, facoltativamente, oggetti di metadati standard e/o personalizzati alla sessione di tracciamento attraverso variabili di dati contestuali.

   * **Metadati standard**

      [Implementazione di metadati standard in javascript](../../../sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >Allegare l'oggetto metadati standard all'oggetto multimediale è facoltativo.

      * Media metadata keys API Reference - [Standard metadata keys - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         See the comprehensive set of available metadata here: [Audio and video parameters](../../../metrics-and-metadata/audio-video-parameters.md)
   * **Metadati personalizzati**

      Creare un oggetto variabile per le variabili personalizzate e compilare i dati per questi contenuti multimediali. Ad esempio:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```


1. **Tenere traccia dell'intenzione di avviare la riproduzione**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >Il secondo valore è il nome dell'oggetto metadati personalizzato creato nel passaggio 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` monitora l'intento utente di riproduzione, non l'inizio della riproduzione. This API is used to load the data/metadata and to estimate the time-to-start QoS metric (the time duration between `trackSessionStart` and `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Tenere traccia dell'inizio effettivo della riproduzione**

   Identify the event from the media player for the beginning of the playback, where the first frame of the media is rendered on the screen, and call `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Tenere traccia del completamento della riproduzione**

   Identify the event from the media player for the completion of the playback, where the user has watched the content until the end, and call `trackComplete`:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Tracciamento della fine della sessione**

   Identify the event from the media player for the unloading/closing of the playback, where the user closes the media and/or the media is completed and has been unloaded, and call `trackSessionEnd`:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >A `trackSessionEnd` marks the end of a tracking session. If the session was successfully watched to completion, where the user watched the content until the end, ensure that `trackComplete` is called before `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.  Metodo di tracciamento della riproduzione multimediale per tenere traccia del caricamento del file multimediale e impostare la sessione corrente su attiva:

   ```
   ‘ Create a media info object
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.id = <MEDIA_ID>
   mediaInfo.playhead = "0"
   mediaInfo.length = "600"
   ```

1. **Allegare metadati video**

   Allegate, facoltativamente, oggetti di metadati video standard e/o personalizzati alla sessione di tracciamento video attraverso variabili di dati contestuali.

   * **Metadati video standard**

      [Implementare i metadati standard su Roku](../../../sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >L'associazione dell'oggetto metadati video standard all'oggetto multimediale è facoltativa.

   * **Metadati personalizzati**

      Creare un oggetto variabile per le variabili personalizzate e compilare i dati per il video. Ad esempio:

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **Tenere traccia dell'intenzione di avviare la riproduzione**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >Il secondo valore è il nome dell'oggetto metadati personalizzato creato nel passaggio 2.

   >[!IMPORTANT]
   >`trackSessionStart` monitora l'intento utente di riproduzione, non l'inizio della riproduzione. This API is used to load the video data/metadata and to estimate the time-to-start QoS metric (the time duration between `trackSessionStart` and `trackPlay`).

   >[!NOTE]
   >If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Tenere traccia dell'inizio effettivo della riproduzione**

   Identify the event from the video player for the beginning of the video playback, where the first frame of the video is rendered on the screen, and call `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **Tenere traccia del completamento della riproduzione**

   Identify the event from the video player for the completion of the video playback, where the user has watched the content until the end, and call `trackComplete`:

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **Tracciamento della fine della sessione**

   Identify the event from the video player for the unloading/closing of the video playback, where the user closes the video and/or the video is completed and has been unloaded, and call `trackSessionEnd`:

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` segna la fine di una sessione di tracciamento video. If the session was successfully watched to completion, where the user watched the content until the end, ensure that `trackComplete` is called before `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **Tenere traccia di tutti i possibili scenari di pausa**

   Identify the event from the video player for video pause and call `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Scenari in pausa**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. The following scenarios all require that your app call `trackPause()`:

   * L'utente si mette in pausa in modo esplicito nell'app.
   * Il lettore si attiva nello stato Pausa.
   * (*Mobile Apps*) - The user puts the application into the background, but you want the app to keep the session open.
   * (*Mobile Apps*) - Any type of system interrupt occurs that causes an application to be backgrounded. Ad esempio, l'utente riceve una chiamata, oppure un pop-up da un'altra applicazione si verifica, ma si desidera che l'applicazione mantenga la sessione viva per consentire all'utente di riprendere il video dal punto di interruzione.

1. Identify the event from the player for video play and/or video resume from pause and call `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >Potrebbe trattarsi della stessa origine dell'evento utilizzata al passaggio 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the video playback resumes.

* Tracking scenarios: [VOD playback with no ads](../../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso con Roku SDK per un esempio di tracciamento completo.

