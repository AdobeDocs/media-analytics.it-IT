---
seo-title: Tracciare la riproduzione di base su Chromecast
title: Tracciare la riproduzione di base su Chromecast
uuid: a 9 fc 59 d 8-a 2 f 4-4889-bdec -55 c 42 a 835 d 06
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Track core playback on Chromecast{#track-core-playback-on-chromecast}

>[!IMPORTANT]
>
>Questa documentazione copre il tracciamento nella versione 2. x dell'SDK. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [Download SDKs](../../../sdk-implement/download-sdks.md)

1. **Configurazione di tracciamento iniziale**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   **`MediaObject`Riferimento API:**

   [Createmediaobject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>); 
   ```

   **`StreamType`costanti:**

   [Adbmobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`costanti:**

   [Adbmobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **Allegare metadati video**

   Allegate, facoltativamente, oggetti di metadati video standard e/o personalizzati alla sessione di tracciamento video attraverso variabili di dati contestuali.

   * **Metadati video standard**

      [Implementare i metadati standard su Chromecast](../../../sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

      >[!NOTE]
      >
      >L'associazione dell'oggetto metadati video standard all'oggetto multimediale è facoltativa.

   * **Metadati personalizzati**

      Creare un oggetto variabile per le variabili personalizzate e compilare i dati per il video. Ad esempio:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```

1. **Tenere traccia dell'intenzione di avviare la riproduzione**

   To begin tracking a media session, call [trackSessionStart](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart) on the `media` object.

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` monitora l'intento utente di riproduzione, non l'inizio della riproduzione. This API is used to load the video data/metadata and to estimate the time-to-start QoS metric (the time duration between `trackSessionStart` and `trackPlay`).

   >[!NOTE]
   >
   >Il secondo valore è il nome dell'oggetto metadati personalizzato creato nel passaggio 2. If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Tenere traccia dell'inizio effettivo della riproduzione**

   Identify the event from the video player for the beginning of the video playback, where the first frame of the video is rendered on the screen, and call [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay)

   ```
   ADBMobile.media.trackPlay();
   ```

1. **Tenere traccia del completamento della riproduzione**

   Identify the event from the video player for the completion of the video playback, where the user has watched the content until the end, and call [trackComplete:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackComplete();
   ```

1. **Tracciamento della fine della sessione**

   Identify the event from the video player for the unloading/closing of the video playback, where the user closes the video and/or the video is completed and has been unloaded, and call [trackSessionEnd:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd)

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` segna la fine di una sessione di tracciamento video. If the session was successfully watched to completion, where the user watched the content until the end, ensure that `trackComplete` is called before `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **Tenere traccia di tutti i possibili scenari di pausa**

   Identify the event from the video player for video pause and call [trackPause:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause)

   ```
   ADBMobile.media.trackPause();
   ```

   **Scenari in pausa**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. The following scenarios all require that your app call `trackPause()`:

   * L'utente si mette in pausa in modo esplicito nell'app.
   * Il lettore si attiva nello stato Pausa.
   * (*Mobile Apps*) - The user puts the application into the background, but you want the app to keep the session open.
   * (*Mobile Apps*) - Any type of system interrupt occurs that causes an application to be backgrounded. Ad esempio, l'utente riceve una chiamata, oppure un pop-up da un'altra applicazione si verifica, ma si desidera che l'applicazione mantenga la sessione viva per consentire all'utente di riprendere il video dal punto di interruzione.

1. Identify the event from the player for video play and/or video resume from pause and call [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >Potrebbe trattarsi della stessa origine dell'evento utilizzata al passaggio 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the video playback resumes.

* Tracking scenarios: [VOD playback with no ads](../../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso con Chromecast SDK per un esempio di tracciamento completo.

