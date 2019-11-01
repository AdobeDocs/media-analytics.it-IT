---
title: Tracciare la riproduzione di base su Android
description: Questo argomento descrive come implementare il tracciamento di base tramite Media SDK su Android.
uuid: ab5fab95-76ed-4ae6-aedb-2e66eece7607
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Tracciare la riproduzione di base su Android{#track-core-playback-on-android}

>[!IMPORTANT]
>Questa documentazione descrive il tracciamento nella versione 2.x dell’SDK. Se stai implementando una versione 1.x dell’SDK, puoi scaricare la guida per sviluppatori 1.x per Android qui: [Download di SDK](/help/sdk-implement/download-sdks.md)

1. **Configurazione iniziale tracciamento**

   Identificare quando l'utente attiva l'intenzione di riproduzione (l'utente fa clic su play e/o la riproduzione automatica è attivata) e creare un' `MediaObject` istanza.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome file multimediale | Sì |
   | `mediaId` | Identificatore univoco del supporto | Sì |
   | `length` | Lunghezza del supporto | Sì |
   | `streamType` | Tipo di flusso (vedere le costanti __ StreamType riportate di seguito) | Sì |
   | `mediaType` | Tipo di supporto (vedere le costanti __ MediaType riportate di seguito) | Sì |

   **`StreamType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `VOD` | Tipo di flusso per Video on Demand. |
   | `LIVE` | Tipo di flusso per il contenuto live. |
   | `LINEAR` | Tipo di flusso per il contenuto lineare. |
   | `AOD` | Tipo di flusso per Audio On Demand |
   | `AUDIOBOOK` | Tipo di flusso per la Rubrica audio |
   | `PODCAST` | Tipo di flusso per Podcast |

   **`MediaType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `Audio` | Tipo di supporto per i flussi audio. |
   | `Video` | Tipo di supporto per i flussi video. |

   ```
   MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
     <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);
   ```

1. **Allega metadati**

   È possibile allegare oggetti metadati standard e/o personalizzati alla sessione di tracciamento tramite variabili di dati di contesto.

   * **Metadati standard**

      [Implementare i metadati standard su Android](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

      >[!NOTE]
      >
      >Il collegamento dell'oggetto metadati standard all'oggetto multimediale è facoltativo.

      * Riferimento API per le chiavi di metadati multimediali - chiavi di metadati [standard - Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * Consultate il set completo di metadati video disponibili qui: Parametri [audio e video](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Metadati personalizzati**

      Create un dizionario per le variabili personalizzate e inserite i dati per questo supporto. Ad esempio:

      ```java
      HashMap<String, String> mediaMetadata =  
        new HashMap<String, String>(); 
      mediaMetadata.put("isUserLoggedIn", "false"); 
      mediaMetadata.put("tvStation", "Sample TV Station"); 
      mediaMetadata.put("programmer", "Sample programmer");
      ```


1. **Tenere traccia dell’intenzione di avviare la riproduzione**

   Per avviare il tracciamento di una sessione multimediale, invocate `trackSessionStart` l’istanza Media Heartbeat. Ad esempio:

   ```java
   public void onVideoLoad(Observable observable, Object data) {  
       _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
   }
   ```

   >[!TIP]
   >
   >Il secondo valore è il nome dell'oggetto metadati multimediale personalizzato creato al punto 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` tiene traccia delle intenzioni dell’utente in merito alla riproduzione, non dell’inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati multimediali e per stimare la metrica QoS time-to-start (la durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzate metadati multimediali personalizzati, inviate semplicemente un oggetto vuoto per il secondo argomento in `trackSessionStart`.

1. **Tracciare l’inizio effettivo della riproduzione**

   Mediante questo componente, potete identificare l’evento dal lettore multimediale per l’inizio della riproduzione, in cui viene riprodotto il primo fotogramma del file multimediale sullo schermo, e chiamare `trackPlay`:

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) { 
       _heartbeat.trackPlay(); 
   }
   ```

1. **Tenere traccia del completamento della riproduzione**

   Identificate l’evento dal lettore multimediale per il completamento della riproduzione, in cui l’utente ha guardato il contenuto fino alla fine, e chiamate `trackComplete`:

   ```java
   public void onVideoComplete(Observable observable, Object data) { 
       _heartbeat.trackComplete(); 
   }
   ```

1. **Tenere traccia della fine della sessione**

   Identificare l’evento dal lettore multimediale per lo scaricamento/la chiusura della riproduzione multimediale, in cui l’utente chiude il supporto e/o il supporto è stato completato e scaricato, e chiamare `trackSessionEnd`:

   ```java
   // Closes the media and/or the media completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd(); 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` segna la fine di una sessione di tracciamento dei supporti. Se la sessione è stata guardata con successo e l’utente ha guardato il contenuto fino alla fine, accertatevi che `trackComplete` venga chiamato prima `trackSessionEnd`. Qualsiasi altra chiamata `track*` API viene ignorata dopo `trackSessionEnd`, fatta eccezione per `trackSessionStart` una nuova sessione di tracciamento dei supporti.

1. **Tenere traccia di tutti gli scenari di pausa possibili**

   Identificare l’evento dal lettore multimediale per la pausa e la chiamata del supporto `trackPause`:

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause(); 
   }
   ```

   **Pausa scenari**

   Identificate eventuali situazioni in cui il lettore video si interrompe e accertatevi che venga chiamato `trackPause` correttamente. Tutti gli scenari seguenti richiedono che la chiamata dell'app `trackPause()`:

   * L'utente interrompe esplicitamente la pausa nell'app.
   * Il lettore si mette nello stato Pausa.
   * (App *mobili*) - L'utente mette l'applicazione in background, ma si desidera che l'app tenga aperta la sessione.
   * (App *mobili*) - Si verifica qualsiasi tipo di interruzione del sistema che causa il background di un'applicazione. Ad esempio, l'utente riceve una chiamata, o si verifica un pop-up da un'altra applicazione, ma si desidera che l'applicazione mantenga in vita la sessione per dare all'utente la possibilità di riprendere il supporto dal punto di interruzione.

1. Identificare l’evento dal lettore per la riproduzione di contenuti multimediali e/o la ripresa di contenuti multimediali dalla pausa e dalla chiamata `trackPlay`.

   ```java
   // trackPlay() 
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay(); 
   }
   ```

   >[!TIP]
   >
   >Può trattarsi della stessa origine evento utilizzata nel passaggio 4. Quando la riproduzione dei contenuti multimediali riprende, accertatevi che ogni chiamata `trackPause()` API sia associata alla seguente chiamata `trackPlay()` API.

Per ulteriori informazioni sul tracciamento della riproduzione di base, consultate:

* Scenari di tracciamento: Riproduzione [VOD senza annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso con Android SDK per un esempio di tracciamento completo.

