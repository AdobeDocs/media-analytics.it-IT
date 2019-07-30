---
seo-title: Tenere traccia della riproduzione di base in javascript
title: Tenere traccia della riproduzione di base in javascript
uuid: 3 d 6 e 0 ab 1-899 a -43 c 3-b 632-8276 e 84345 ab
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Track core playback on JavaScript{#track-core-playback-on-javascript}

>[!IMPORTANT]
>Questa documentazione copre il tracciamento nella versione 2. x dell'SDK. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [Download SDKs](/help/sdk-implement/download-sdks.md)

1. **Configurazione di tracciamento iniziale**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [API createmediaobject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome file multimediali | Sì |
   | `mediaid` | Identificatore univoco multimediale | Sì |
   | `length` | Lunghezza media | Sì |
   | `streamType` | Stream type (see _StreamType constants_ below) | Sì |
   | `mediaType` | Media type (see _MediaType constants_ below) | Sì |

   **`StreamType`costanti:**

   | Nome costante | Descrizione   |
   |---|---|
   | `VOD` | Tipo di flusso per Video su richiesta. |
   | `LIVE` | Tipo di flusso per il contenuto LIVE. |
   | `LINEAR` | Tipo di flusso per il contenuto lineare. |
   | `AOD` | Tipo di flusso per l'audio su richiesta. |
   | `AUDIOBOOK` | Tipo di flusso per il libro audio. |
   | `PODCAST` | Tipo di flusso per Podcast. |

   **`MediaType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `Audio` | Tipo di file multimediale per i flussi audio. |
   | `Video` | Tipo di supporto per i flussi video. |

   ```
   var mediaObject =  
     MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>, 
                                     MediaHeartbeat.StreamType.VOD,
                                     <MEDIA_TYPE>);
   ```

1. **Allega metadati**

   Allega, facoltativamente, oggetti di metadati standard e/o personalizzati alla sessione di tracciamento attraverso variabili di dati contestuali.

   * **Metadati standard**

      [Implementazione di metadati standard in javascript](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >Allegare l'oggetto metadati standard all'oggetto multimediale è facoltativo.

      * Media metadata keys API Reference - [Standard metadata keys - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         See the comprehensive set of available metadata here: [Audio and video parameters](/help/metrics-and-metadata/audio-video-parameters.md)
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
   >`trackSessionEnd` segna la fine di una sessione di tracciamento. If the session was successfully watched to completion, where the user watched the content until the end, ensure that `trackComplete` is called before `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.

1. **Tenere traccia di tutti i possibili scenari di pausa**

   Identify the event from the media player for pause and call `trackPause`:

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Scenari in pausa**

   Identify any scenario in which the media player will pause and make sure that `trackPause` is properly called. The following scenarios all require that your app call `trackPause()`:

   * L'utente si mette in pausa in modo esplicito nell'app.
   * Il lettore si attiva nello stato Pausa.
   * (*Mobile Apps*) - The user puts the application into the background, but you want the app to keep the session open.
   * (*Mobile Apps*) - Any type of system interrupt occurs that causes an application to be backgrounded. Ad esempio, l'utente riceve una chiamata, oppure un pop-up da un'altra applicazione si verifica, ma si desidera che l'applicazione mantenga la sessione viva per consentire all'utente di riprendere i contenuti multimediali dal punto di interruzione.

1. Identify the event from the player for play and/or resume from pause and call `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >Potrebbe trattarsi della stessa origine dell'evento utilizzata al passaggio 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the playback resumes.

* Tracking scenarios: [VOD playback with no ads](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso con javascript SDK per un esempio di tracciamento completo.

