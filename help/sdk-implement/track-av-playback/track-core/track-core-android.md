---
seo-title: Tenere traccia della riproduzione di base su Android
title: Tenere traccia della riproduzione di base su Android
uuid: ab 5 fab 95-76 ed -4 ae 6-aedb -2 e 66 emask 7607
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Track core playback on Android{#track-core-playback-on-android}

>[!IMPORTANT]
>Questa documentazione copre il tracciamento nella versione 2. x dell'SDK. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guide for Android here: [Download SDKs](/help/sdk-implement/download-sdks.md)

1. **Configurazione di tracciamento iniziale**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [API createmediaobject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome file multimediali | Sì |
   | `mediaId` | Identificatore univoco multimediale | Sì |
   | `length` | Lunghezza media | Sì |
   | `streamType` | Stream type (see _StreamType constants_ below) | Sì |
   | `mediaType` | Media type (see _MediaType constants_ below) | Sì |

   **`StreamType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `VOD` | Tipo di flusso per Video su richiesta. |
   | `LIVE` | Tipo di flusso per il contenuto Live. |
   | `LINEAR` | Tipo di flusso per il contenuto lineare. |
   | `AOD` | Tipo di flusso per Audio on demand |
   | `AUDIOBOOK` | Tipo di flusso per il libro audio |
   | `PODCAST` | Tipo di flusso per Podcast |

   **`MediaType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `Audio` | Tipo di file multimediale per i flussi audio. |
   | `Video` | Tipo di supporto per i flussi video. |

   ```
   MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
     <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);
   ```

1. **Allega metadati**

   Allega, facoltativamente, oggetti di metadati standard e/o personalizzati alla sessione di tracciamento attraverso variabili di dati contestuali.

   * **Metadati standard**

      [Implementare i metadati standard su Android](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

      >[!NOTE]
      >
      >Allegare l'oggetto metadati standard all'oggetto multimediale è facoltativo.

      * Media metadata keys API Reference - [Standard metadata keys - Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * See the comprehensive set of available video metadata here: [Audio and video parameters](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Metadati personalizzati**

      Creare un dizionario per le variabili personalizzate e compilare i dati per questi contenuti multimediali. Ad esempio:

      ```java
      HashMap<String, String> mediaMetadata =  
        new HashMap<String, String>(); 
      mediaMetadata.put("isUserLoggedIn", "false"); 
      mediaMetadata.put("tvStation", "Sample TV Station"); 
      mediaMetadata.put("programmer", "Sample programmer");
      ```


1. **Tenere traccia dell'intenzione di avviare la riproduzione**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance. Ad esempio:

   ```java
   public void onVideoLoad(Observable observable, Object data) {  
       _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
   }
   ```

   >[!TIP]
   >
   >Il secondo valore è il nome dell'oggetto metadati personalizzato creato nel passaggio 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` monitora l'intento utente di riproduzione, non l'inizio della riproduzione. This API is used to load the media data/metadata and to estimate the time-to-start QoS metric (the time duration between `trackSessionStart` and `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom media metadata, simply send an empty object for the second argument in `trackSessionStart`.

1. **Tenere traccia dell'inizio effettivo della riproduzione**

   Identify the event from the media player for the beginning of the media playback, where the first frame of the media is rendered on the screen, and call `trackPlay`:

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) { 
       _heartbeat.trackPlay(); 
   }
   ```

1. **Tenere traccia del completamento della riproduzione**

   Identify the event from the media player for the completion of the media playback, where the user has watched the content until the end, and call `trackComplete`:

   ```java
   public void onVideoComplete(Observable observable, Object data) { 
       _heartbeat.trackComplete(); 
   }
   ```

1. **Tracciamento della fine della sessione**

   Identify the event from the media player for the unloading/closing of the media playback, where the user closes the media and/or the media is completed and has been unloaded, and call `trackSessionEnd`:

   ```java
   // Closes the media and/or the media completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd(); 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` segna la fine di una sessione di tracciamento multimediale. If the session was successfully watched to completion, where the user watched the content until the end, ensure that `trackComplete` is called before `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new media tracking session.

1. **Tenere traccia di tutti i possibili scenari di pausa**

   Identify the event from the media player for media pause and call `trackPause`:

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause(); 
   }
   ```

   **Scenari in pausa**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. The following scenarios all require that your app call `trackPause()`:

   * L'utente si mette in pausa in modo esplicito nell'app.
   * Il lettore si attiva nello stato Pausa.
   * (*Mobile Apps*) - The user puts the application into the background, but you want the app to keep the session open.
   * (*Mobile Apps*) - Any type of system interrupt occurs that causes an application to be backgrounded. Ad esempio, l'utente riceve una chiamata, oppure un pop-up da un'altra applicazione si verifica, ma si desidera che l'applicazione mantenga la sessione viva per consentire all'utente di riprendere i contenuti multimediali dal punto di interruzione.

1. Identify the event from the player for media play and/or media resume from pause and call `trackPlay`.

   ```java
   // trackPlay() 
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay(); 
   }
   ```

   >[!TIP]
   >
   >Potrebbe trattarsi della stessa origine dell'evento utilizzata al passaggio 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the media playback resumes.

Per ulteriori informazioni sulla riproduzione di base di tracciamento, consultate quanto segue:

* Tracking scenarios: [VOD playback with no ads](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso con Android SDK per un esempio di tracciamento completo.

