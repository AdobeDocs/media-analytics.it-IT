---
seo-title: Tracciare la riproduzione di base su Roku
title: Tracciare la riproduzione di base su Roku
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tracciare la riproduzione di base su Roku{#track-core-playback-on-roku}

>[!IMPORTANT]
>Questa documentazione descrive il tracciamento nella versione 2.x dell’SDK. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Download di SDK](/help/sdk-implement/download-sdks.md)

1. **Configurazione iniziale tracciamento**

   Identificare quando l'utente attiva l'intenzione di riproduzione (l'utente fa clic su play e/o la riproduzione automatica è attivata) e creare un' `MediaObject` istanza.

   **`MediaObject`riferimento:**

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome video | Sì |
   | `mediaid` | Identificatore univoco video | Sì |
   | `length` | Lunghezza video | Sì |
   | `streamType` | Tipo di flusso (vedere le costanti __ StreamType riportate di seguito) | Sì |
   | `mediaType` | Tipo di supporto (vedere le costanti __ MediaType riportate di seguito) | Sì |

   **`StreamType`costanti:**

   | Nome costante | Descrizione   |
   |---|---|
   | `MEDIA_STREAM_TYPE_VOD` | Tipo di flusso per Video on Demand. |
   | `MEDIA_STREAM_TYPE_LIVE` | Tipo di flusso per il contenuto LIVE. |
   | `MEDIA_STREAM_TYPE_LINEAR` | Tipo di flusso per il contenuto LINEAR. |
   | `MEDIA_STREAM_TYPE_AOD` | Tipo di flusso per Audio On Demand |
   | `MEDIA_STREAM_TYPE_AUDIOBOOK` | Tipo di flusso per la Rubrica audio |
   | `MEDIA_STREAM_TYPE_PODCAST` | Tipo di flusso per Podcast |

   **`MediaType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `MEDIA_STREAM_TYPE_AUDIO` | Tipo di supporto per i flussi audio. |
   | `MEDIA_STREAM_TYPE_VIDEO` | Tipo di supporto per i flussi video. |

   **Create un oggetto media info per il video con contenuto VOD:**

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

   **Create un oggetto media info per il video con contenuto AOD:**

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

   È possibile allegare oggetti metadati standard e/o personalizzati alla sessione di tracciamento tramite variabili di dati di contesto.

   * **Metadati standard**

      [Implementare i metadati standard in JavaScript](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >Il collegamento dell'oggetto metadati standard all'oggetto multimediale è facoltativo.

      * Riferimento API per le chiavi di metadati multimediali - chiavi di metadati [standard - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         Consultate il set completo dei metadati disponibili qui: Parametri [audio e video](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Metadati personalizzati**

      Create un oggetto variabile per le variabili personalizzate e inserite i dati per questo supporto. Ad esempio:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```


1. **Tenere traccia dell’intenzione di avviare la riproduzione**

   Per avviare il tracciamento di una sessione multimediale, invocate `trackSessionStart` l’istanza Media Heartbeat:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >Il secondo valore è il nome dell'oggetto metadati multimediale personalizzato creato al punto 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` tiene traccia delle intenzioni dell’utente in merito alla riproduzione, non dell’inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati e per stimare la metrica QoS time-to-start (la durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzate metadati personalizzati, inviate semplicemente un oggetto vuoto per l' `data` argomento in `trackSessionStart`, come mostrato nella riga commento nell'esempio iOS precedente.

1. **Tracciare l’inizio effettivo della riproduzione**

   Identificate l’evento dal lettore multimediale per l’inizio della riproduzione, dove viene riprodotto il primo fotogramma del file multimediale sullo schermo, e chiamate `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Tenere traccia del completamento della riproduzione**

   Identificate l’evento dal lettore multimediale per il completamento della riproduzione, in cui l’utente ha guardato il contenuto fino alla fine, e chiamate `trackComplete`:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Tenere traccia della fine della sessione**

   Identificare l’evento dal lettore multimediale per lo scaricamento/la chiusura della riproduzione, in cui l’utente chiude il supporto e/o il supporto è stato completato e scaricato, e chiamare `trackSessionEnd`:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >Una `trackSessionEnd` indica la fine di una sessione di tracciamento. Se la sessione è stata guardata con successo e l’utente ha guardato il contenuto fino alla fine, accertatevi che `trackComplete` venga chiamato prima `trackSessionEnd`. Qualsiasi altra chiamata `track*` API viene ignorata dopo `trackSessionEnd`, fatta eccezione per `trackSessionStart` una nuova sessione di tracciamento.  Metodo di tracciamento della riproduzione multimediale per tenere traccia del carico multimediale e impostare la sessione corrente su attiva:

   ```
   ‘ Create a media info object
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.id = <MEDIA_ID>
   mediaInfo.playhead = "0"
   mediaInfo.length = "600"
   ```

1. **Allega metadati video**

   Facoltativamente, potete allegare oggetti di metadati video standard e/o personalizzati alla sessione di tracciamento video tramite variabili di dati contestuali.

   * **Metadati video standard**

      [Implementare i metadati standard su Roku](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >Il collegamento dell'oggetto di metadati video standard all'oggetto multimediale è facoltativo.

   * **Metadati personalizzati**

      Create un oggetto variabile per le variabili personalizzate e inserite i dati per questo video. Ad esempio:

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **Tenere traccia dell’intenzione di avviare la riproduzione**

   Per avviare il tracciamento di una sessione multimediale, invocate `trackSessionStart` l’istanza Media Heartbeat:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >Il secondo valore è il nome dell'oggetto di metadati video personalizzato creato al punto 2.

   >[!IMPORTANT]
   >`trackSessionStart` tiene traccia delle intenzioni dell’utente in merito alla riproduzione, non dell’inizio della riproduzione. Questa API viene utilizzata per caricare i dati video/metadati e per stimare la metrica QoS time-to-start (la durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >Se non utilizzate metadati video personalizzati, inviate semplicemente un oggetto vuoto per l' `data` argomento in `trackSessionStart`, come illustrato nella riga commento nell'esempio iOS precedente.

1. **Tracciare l’inizio effettivo della riproduzione**

   Identificate l’evento dal lettore video per l’inizio della riproduzione del video, dove viene riprodotto il primo fotogramma del video sullo schermo, e chiamate `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **Tenere traccia del completamento della riproduzione**

   Individuate l’evento dal lettore video al termine della riproduzione video, in cui l’utente ha guardato il contenuto fino alla fine, e chiamate `trackComplete`:

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **Tenere traccia della fine della sessione**

   Mediante questo componente, potete identificare l’evento dal lettore video per lo scaricamento/la chiusura della riproduzione video, in cui l’utente chiude il video e/o il video viene completato ed è stato scaricato e chiamare `trackSessionEnd`:

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` segna la fine di una sessione di tracciamento video. Se la sessione è stata guardata con successo e l’utente ha guardato il contenuto fino alla fine, accertatevi che `trackComplete` venga chiamato prima `trackSessionEnd`. Qualsiasi altra chiamata `track*` API viene ignorata dopo `trackSessionEnd`, fatta eccezione per `trackSessionStart` una nuova sessione di tracciamento video.

1. **Tenere traccia di tutti gli scenari di pausa possibili**

   Identificate l’evento dal lettore video per la pausa video e chiamate `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Pausa scenari**

   Identificate eventuali situazioni in cui il lettore video si interrompe e accertatevi che venga chiamato `trackPause` correttamente. Tutti gli scenari seguenti richiedono che la chiamata dell'app `trackPause()`:

   * L'utente interrompe esplicitamente la pausa nell'app.
   * Il lettore si mette nello stato Pausa.
   * (App *mobili*) - L'utente mette l'applicazione in background, ma si desidera che l'app tenga aperta la sessione.
   * (App *mobili*) - Si verifica qualsiasi tipo di interruzione del sistema che causa il background di un'applicazione. Ad esempio, l'utente riceve una chiamata, o si verifica un pop-up da un'altra applicazione, ma si desidera che l'applicazione mantenga in vita la sessione per dare all'utente la possibilità di riprendere il video dal punto di interruzione.

1. Identificare l’evento dal lettore per la riproduzione video e/o la ripresa video dalla pausa e dalla chiamata `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >Può trattarsi della stessa origine evento utilizzata nel passaggio 4. Quando la riproduzione del video riprende, accertatevi che ogni chiamata `trackPause()` API sia associata a una chiamata `trackPlay()` API seguente.

* Scenari di tracciamento: Riproduzione [VOD senza annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso con Roku SDK per un esempio di tracciamento completo.

