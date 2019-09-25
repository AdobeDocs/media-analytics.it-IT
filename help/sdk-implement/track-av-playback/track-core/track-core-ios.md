---
seo-title: Tracciare la riproduzione di base su iOS
title: Tracciare la riproduzione di base su iOS
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tracciare la riproduzione di base su iOS{#track-core-playback-on-ios}

>[!IMPORTANT]
>Questa documentazione descrive il tracciamento nella versione 2.x dell’SDK. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Download di SDK](/help/sdk-implement/download-sdks.md)

1. **Configurazione iniziale tracciamento**

   Identificare quando l'utente attiva l'intenzione di riproduzione (l'utente fa clic su play e/o la riproduzione automatica è attivata) e creare un' `MediaObject` istanza.

   [API createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | Nome della variabile | Descrizione | Obbligatorio |
   |---|---|---|
   | `name` | Nome video | Sì |
   | `mediaid` | Identificatore univoco video | Sì |
   | `length` | Lunghezza video | Sì |
   | `streamType` | Tipo di flusso (vedere le costanti __ StreamType riportate di seguito) | Sì |
   | `mediaType` | Tipo di supporto (vedere le costanti __ MediaType riportate di seguito) | Sì |

   **`StreamType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | Tipo di flusso per video su richiesta |
   | `ADBMediaHeartbeatStreamTypeLIVE` | Tipo di flusso per il contenuto live |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | Tipo di flusso per il contenuto lineare |
   | `ADBMediaHeartbeatStreamTypeAOD` | Tipo di flusso per Audio On Demand |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | Tipo di flusso per la Rubrica audio |
   | `ADBMediaHeartbeatStreamTypePODCAST` | Tipo di flusso per Podcast |

   **`MediaType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `ADBMediaTypeAudio` | Tipo di supporto per i flussi audio. |
   | `ADBMediaTypeVideo` | Tipo di supporto per i flussi video. |

   Formato generale per la creazione di `MediaObject`:

   ```
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME> 
                                          mediaId:<MEDIA_ID> 
                                           length:<MEDIA_LENGTH>                       
                                       streamType:<STREAM_TYPE> 
                                        mediaType: <MEDIA_TYPE>];
   ```

1. **Allega metadati video**

   Facoltativamente, potete allegare oggetti di metadati video standard e/o personalizzati alla sessione di tracciamento video tramite variabili di dati contestuali.

   * **Metadati video standard**

      * [Implementazione di metadati standard su iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **Tasti di metadati video**
         [Chiavi di metadati iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * Consultate l'elenco completo dei metadati video, qui: Parametri [audio e video](/help/metrics-and-metadata/audio-video-parameters.md)
      >[!NOTE]
      >
      >Il collegamento dell'oggetto di metadati video standard all'oggetto multimediale è facoltativo.

   * **Metadati personalizzati**

      Create un oggetto variabile per le variabili personalizzate e inserite i dati per questo video. Ad esempio:

      ```
      NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init]; 
      [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"]; 
      [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
      ```


1. **Tenere traccia dell’intenzione di avviare la riproduzione**

   Per avviare il tracciamento di una sessione multimediale, invocate `trackSessionStart` l’istanza Media Heartbeat.

   >[!TIP]
   >
   >Il secondo valore è il nome dell'oggetto di metadati video personalizzato creato al punto 2.

   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification { 
   //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil]; 
       [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` tiene traccia delle intenzioni dell’utente in merito alla riproduzione, non dell’inizio della riproduzione. Questa API viene utilizzata per caricare i dati video/metadati e per stimare la metrica QoS time-to-start (la durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzate metadati video personalizzati, inviate semplicemente un oggetto vuoto per l' `data` argomento in `trackSessionStart`, come illustrato nella riga commento nell'esempio iOS precedente.

1. **Tracciare l’inizio effettivo della riproduzione**

   Identificate l’evento dal lettore video per l’inizio della riproduzione del video, dove viene riprodotto il primo fotogramma del video sullo schermo, e chiamate `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

1. **Tenere traccia del completamento della riproduzione**

   Individuate l’evento dal lettore video al termine della riproduzione video, in cui l’utente ha guardato il contenuto fino alla fine, e chiamate `trackComplete`:

   ```
   - (void)onVideoComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackComplete]; 
   }
   ```

1. **Tenere traccia della fine della sessione**

   Mediante questo componente, potete identificare l’evento dal lettore video per lo scaricamento/la chiusura della riproduzione video, in cui l’utente chiude il video e/o il video viene completato ed è stato scaricato e chiamare `trackSessionEnd`:

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification { 
       [_mediaHeartbeat trackSessionEnd]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` segna la fine di una sessione di tracciamento video. Se la sessione è stata guardata con successo e l’utente ha guardato il contenuto fino alla fine, accertatevi che `trackComplete` venga chiamato prima `trackSessionEnd`. Qualsiasi altra chiamata `track*` API viene ignorata dopo `trackSessionEnd`, fatta eccezione per `trackSessionStart` una nuova sessione di tracciamento video.

1. **Tenere traccia di tutti gli scenari di pausa possibili**

   Identificate l’evento dal lettore video per la pausa video e chiamate `trackPause`:

   ```
   - (void)onVideoPause:(NSNotification *)notification { 
       [_mediaHeartbeat trackPause]; 
   }
   ```

   **Pausa scenari**

   Identificate eventuali situazioni in cui il lettore video si interrompe e accertatevi che venga chiamato `trackPause` correttamente. Tutti gli scenari seguenti richiedono che la chiamata dell'app `trackPause()`:

   * L'utente interrompe esplicitamente la pausa nell'app.
   * Il lettore si mette nello stato Pausa.
   * (App *mobili*) - L'utente mette l'applicazione in background, ma si desidera che l'app tenga aperta la sessione.
   * (App *mobili*) - Si verifica qualsiasi tipo di interruzione del sistema che causa il background di un'applicazione. Ad esempio, l'utente riceve una chiamata, o si verifica un pop-up da un'altra applicazione, ma si desidera che l'applicazione mantenga in vita la sessione per dare all'utente la possibilità di riprendere il video dal punto di interruzione.

1. Identificare l’evento dal lettore per la riproduzione video e/o la ripresa video dalla pausa e dalla chiamata `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

   >[!TIP]
   >
   >Può trattarsi della stessa origine evento utilizzata nel passaggio 4. Quando la riproduzione del video riprende, accertatevi che ogni chiamata `trackPause()` API sia associata a una chiamata `trackPlay()` API seguente.

Per ulteriori informazioni sul tracciamento della riproduzione di base, consultate:

* Scenari di tracciamento: Riproduzione [VOD senza annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso con l’SDK iOS per un esempio di tracciamento completo.

