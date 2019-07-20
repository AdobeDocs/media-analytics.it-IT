---
seo-title: Tracciare la riproduzione di base su iOS
title: Tracciare la riproduzione di base su iOS
uuid: bdc 0 e 05 c -4 fe 5-430 e-aee 2-f 331 bc 59 ac 6 b
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Track core playback on iOS{#track-core-playback-on-ios}

>[!IMPORTANT]
>Questa documentazione copre il tracciamento nella versione 2. x dell'SDK. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [Download SDKs](../../../sdk-implement/download-sdks.md)

1. **Configurazione di tracciamento iniziale**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [API createmediaobjectwithname](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | Nome della variabile | Descrizione | Obbligatorio |
   |---|---|---|
   | `name` | Nome video | Sì |
   | `mediaid` | Identificatore univoco video | Sì |
   | `length` | Lunghezza video | Sì |
   | `streamType` | Stream type (see _StreamType constants_ below) | Sì |
   | `mediaType` | Media type (see _MediaType constants_ below) | Sì |

   **`StreamType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | Tipo di flusso per Video su richiesta |
   | `ADBMediaHeartbeatStreamTypeLIVE` | Tipo di flusso per il contenuto live |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | Tipo di flusso per contenuto lineare |
   | `ADBMediaHeartbeatStreamTypeAOD` | Tipo di flusso per Audio on demand |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | Tipo di flusso per il libro audio |
   | `ADBMediaHeartbeatStreamTypePODCAST` | Tipo di flusso per Podcast |

   **`MediaType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `ADBMediaTypeAudio` | Tipo di file multimediale per i flussi audio. |
   | `ADBMediaTypeVideo` | Tipo di supporto per i flussi video. |

   The general format for creating the `MediaObject`:

   ```
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME> 
                                          mediaId:<MEDIA_ID> 
                                           length:<MEDIA_LENGTH>                       
                                       streamType:<STREAM_TYPE> 
                                        mediaType: <MEDIA_TYPE>];
   ```

1. **Allegare metadati video**

   Allegate, facoltativamente, oggetti di metadati video standard e/o personalizzati alla sessione di tracciamento video attraverso variabili di dati contestuali.

   * **Metadati video standard**

      * [Implementare i metadati standard su iOS](../../../sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **Tasti di metadati video**
         [Chiavi di metadati iOS](../../../sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * See the comprehensive list of video metadata here: [Audio and video parameters](../../../metrics-and-metadata/audio-video-parameters.md)
      >[!NOTE]
      >
      >L'associazione dell'oggetto metadati video standard all'oggetto multimediale è facoltativa.

   * **Metadati personalizzati**

      Creare un oggetto variabile per le variabili personalizzate e compilare i dati per il video. Ad esempio:

      ```
      NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init]; 
      [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"]; 
      [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
      ```


1. **Tenere traccia dell'intenzione di avviare la riproduzione**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance.

   >[!TIP]
   >
   >Il secondo valore è il nome dell'oggetto metadati personalizzato creato nel passaggio 2.

   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification { 
   //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil]; 
       [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` monitora l'intento utente di riproduzione, non l'inizio della riproduzione. This API is used to load the video data/metadata and to estimate the time-to-start QoS metric (the time duration between `trackSessionStart` and `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Tenere traccia dell'inizio effettivo della riproduzione**

   Identify the event from the video player for the beginning of the video playback, where the first frame of the video is rendered on the screen, and call `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

1. **Tenere traccia del completamento della riproduzione**

   Identify the event from the video player for the completion of the video playback, where the user has watched the content until the end, and call `trackComplete`:

   ```
   - (void)onVideoComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackComplete]; 
   }
   ```

1. **Tracciamento della fine della sessione**

   Identify the event from the video player for the unloading/closing of the video playback, where the user closes the video and/or the video is completed and has been unloaded, and call `trackSessionEnd`:

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification { 
       [_mediaHeartbeat trackSessionEnd]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` segna la fine di una sessione di tracciamento video. If the session was successfully watched to completion, where the user watched the content until the end, ensure that `trackComplete` is called before `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **Tenere traccia di tutti i possibili scenari di pausa**

   Identify the event from the video player for video pause and call `trackPause`:

   ```
   - (void)onVideoPause:(NSNotification *)notification { 
       [_mediaHeartbeat trackPause]; 
   }
   ```

   **Scenari in pausa**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. The following scenarios all require that your app call `trackPause()`:

   * L'utente si mette in pausa in modo esplicito nell'app.
   * Il lettore si attiva nello stato Pausa.
   * (*Mobile Apps*) - The user puts the application into the background, but you want the app to keep the session open.
   * (*Mobile Apps*) - Any type of system interrupt occurs that causes an application to be backgrounded. Ad esempio, l'utente riceve una chiamata, oppure un pop-up da un'altra applicazione si verifica, ma si desidera che l'applicazione mantenga la sessione viva per consentire all'utente di riprendere il video dal punto di interruzione.

1. Identify the event from the player for video play and/or video resume from pause and call `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

   >[!TIP]
   >
   >Potrebbe trattarsi della stessa origine dell'evento utilizzata al passaggio 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the video playback resumes.

Per ulteriori informazioni sulla riproduzione di base di tracciamento, consultate quanto segue:

* Tracking scenarios: [VOD playback with no ads](../../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso con iOS SDK per un esempio di tracciamento completo.

