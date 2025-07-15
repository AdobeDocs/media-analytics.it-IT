---
title: Scopri come tenere traccia della riproduzione di base su Android
description: Scopri come implementare il tracciamento di base utilizzando Media SDK su Android.
uuid: ab5fab95-76ed-4ae6-aedb-2e66eece7607
exl-id: d5f5a3f0-f1e0-4d68-af7f-88a30faed0db
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 100%

---

# Tracciare la riproduzione di base su Android{#track-core-playback-on-android}

Questa documentazione tratta il tracciamento nella versione 2.x dell’SDK.
>[!IMPORTANT]
>
>Se stai implementando una versione 1.x dell’SDK, puoi scaricare la Guida per gli sviluppatori 1.x per Android qui: [Scaricare gli SDK](/help/getting-started/download-sdks.md)

1. **Configurazione del tracciamento iniziale**

   Identifica quando l’utente attiva l’intenzione di riproduzione (l’utente fa clic su play e/o l’esecuzione automatica è attiva) e crea un’istanza `MediaObject`.

   [API createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | Nome variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome file multimediale | Sì |
   | `mediaId` | Identificatore univoco del file multimediale | Sì |
   | `length` | Lunghezza del file multimediale | Sì |
   | `streamType` | Tipo di flusso (vedi _Costanti StreamType_ sotto) | Sì |
   | `mediaType` | Tipo di file multimediale (vedi _Costanti MediaType_ sotto) | Sì |

   **`StreamType`Costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `VOD` | Tipo di flusso per Video on Demand. |
   | `LIVE` | Tipo di flusso per il contenuto Live. |
   | `LINEAR` | Tipo di flusso per contenuti Linear. |
   | `AOD` | Tipo di flusso per audio on-demand |
   | `AUDIOBOOK` | Tipo di flusso per audiolibro |
   | `PODCAST` | Tipo di flusso per Podcast |

   **`MediaType`Costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `Audio` | Tipo di file multimediale per flussi Audio. |
   | `Video` | Tipo di file multimediale per i flussi Video. |

   ```
   MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
     <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);
   ```

1. **Allega metadati**

   Facoltativamente, allega oggetti metadati standard e/o personalizzati alla sessione di tracciamento tramite variabili di dati di contesto.

   * **Metadati standard**

     [Implementazione dei metadati standard su Android](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

     >[!NOTE]
     >
     >Il collegamento dell’oggetto metadati standard all’oggetto multimediale è facoltativo.

      * Riferimento API per le chiavi di metadati multimediali - [Chiavi metadati standard - Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * Vedi il set completo di metadati video disponibili qui: [Parametri audio e video](/help/implementation/variables/audio-video-parameters.md)

   * **Metadati personalizzati**

     Crea un dizionario per le variabili personalizzate e compilalo con i dati per questo file multimediale. Ad esempio:

     ```java
     HashMap<String, String> mediaMetadata =  
       new HashMap<String, String>();
     mediaMetadata.put("isUserLoggedIn", "false");
     mediaMetadata.put("tvStation", "Sample TV Station");
     mediaMetadata.put("programmer", "Sample programmer");
     ```

1. **Tracciare l’intenzione di avviare la riproduzione**

   Per iniziare a tracciare una sessione multimediale, chiama `trackSessionStart` sull’istanza Media Heartbeat. Ad esempio:

   ```java
   public void onVideoLoad(Observable observable, Object data) {  
       _heartbeat.trackSessionStart(mediaInfo, mediaMetadata);
   }
   ```

   >[!TIP]
   >
   >Il secondo valore è il nome dell’oggetto metadati multimediali personalizzati creato al passaggio 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` tiene traccia delle intenzioni di riproduzione dell’utente, non dell’inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati multimediali e per stimare la metrica QoS del tempo per l’avvio (la durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzi metadati multimediali personalizzati, è sufficiente inviare un oggetto vuoto per il secondo argomento in `trackSessionStart`.

1. **Tracciare l’inizio effettivo della riproduzione**

   Identifica l’evento dal lettore multimediale relativo all’inizio della riproduzione, dove viene eseguito il rendering del primo fotogramma del contenuto multimediale sullo schermo, e chiama `trackPlay`:

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) {
       _heartbeat.trackPlay();
   }
   ```

1. **Tracciare il completamento della riproduzione**

   Identifica l’evento dal lettore multimediale relativo al completamento della riproduzione multimediale, in cui l’utente ha guardato il contenuto fino alla fine, e chiama `trackComplete`:

   ```java
   public void onVideoComplete(Observable observable, Object data) {
       _heartbeat.trackComplete();
   }
   ```

1. **Tracciare la fine della sessione**

   Identifica l’evento dal lettore multimediale relativo allo scaricamento/chiusura della riproduzione multimediale, in cui l’utente chiude il contenuto multimediale e/o il contenuto viene completato e scaricato, e chiama `trackSessionEnd`:

   ```java
   // Closes the media and/or the media completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd();
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` contrassegna il termine di una sessione di tracciamento dei contenuti multimediali. Se la sessione è stata guardata correttamente fino al completamento, in cui l’utente ha guardato il contenuto fino alla fine, assicurati che `trackComplete` venga chiamato prima di `trackSessionEnd`. Qualsiasi altra chiamata API `track*` viene ignorata dopo `trackSessionEnd`, tranne `trackSessionStart` per una nuova sessione di tracciamento dei contenuti multimediali.

1. **Tracciare tutti i possibili scenari di pausa**

   Identifica l’evento dal lettore multimediale relativo alla sospensione del contenuto multimediale e chiama `trackPause`:

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause();
   }
   ```

   **Scenari di sospensione**

   Identifica uno scenario in cui il lettore video si interrompe e verifica che `trackPause` sia chiamato correttamente. I seguenti scenari richiedono tutti una chiamata `trackPause()` dall’app:

   * L’utente mette esplicitamente in pausa l’app.
   * Il lettore si mette in pausa da solo.
   * (*App per dispositivi mobili*): l’utente mette l’applicazione in background, ma si desidera invece che l’app mantenga aperta la sessione.
   * (*App per dispositivi mobili*) - Può verificarsi qualsiasi tipo di interruzione di sistema che porta l’applicazione in background. Ad esempio, l’utente riceve una chiamata oppure la notifica da un’altra applicazione, ma desideri che l’applicazione mantenga aperta la sessione per dare all’utente l’opportunità di riprendere l’elemento multimediale dal punto in cui è stato interrotto.

1. Identifica l’evento dal lettore relativo alla riproduzione e/o la ripresa di contenuti multimediali dalla sospensione e chiama `trackPlay`.

   ```java
   // trackPlay()
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay();
   }
   ```

   >[!TIP]
   >
   >Potrebbe trattarsi della stessa origine evento utilizzata nel passaggio 4. Assicurati che ogni chiamata API di `trackPause()` sia associata alla successiva chiamata API di `trackPlay()` quando la riproduzione multimediale riprende.

Per ulteriori informazioni sul tracciamento della riproduzione core, consulta:

* Scenari di tracciamento: [riproduzione VOD senza annunci](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso nell’SDK di Android per un esempio di tracciamento completo.
