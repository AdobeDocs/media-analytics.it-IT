---
title: Scopri come tenere traccia della riproduzione core su iOS
description: Scopri come implementare il tracciamento di base utilizzando Media SDK su iOS.
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
exl-id: 5c6b36b3-a421-45a4-a65e-4eb57513ca4a
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 2%

---

# Tracciamento riproduzione core su iOS{#track-core-playback-on-ios}

Questa documentazione tratta il tracciamento nella versione 2.x dell&#39;SDK.

>[!IMPORTANT]
>Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK](/help/sdk-implement/download-sdks.md)

1. **Configurazione del tracciamento iniziale**

   Identifica quando l&#39;utente attiva l&#39;intenzione di riproduzione (l&#39;utente fa clic su play e/o autoplay è attivato) e crea un&#39;istanza `MediaObject`.

   [API createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | Nome variable | Descrizione | Obbligatorio |
   |---|---|---|
   | `name` | Nome video | Sì |
   | `mediaid` | Identificatore univoco del video | Sì |
   | `length` | Lunghezza del video | Sì |
   | `streamType` | Tipo di flusso (vedere _Costanti StreamType_ di seguito) | Sì |
   | `mediaType` | Tipo di supporto (vedi _Costanti MediaType_ di seguito) | Sì |

   **`StreamType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | Tipo di flusso per video on Demand |
   | `ADBMediaHeartbeatStreamTypeLIVE` | Tipo di flusso per il contenuto live |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | Tipo di flusso per il contenuto lineare |
   | `ADBMediaHeartbeatStreamTypeAOD` | Tipo di flusso per Audio On Demand |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | Tipo di flusso per audio book |
   | `ADBMediaHeartbeatStreamTypePODCAST` | Tipo di flusso per Podcast |

   **`MediaType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `ADBMediaTypeAudio` | Tipo di supporto per flussi audio. |
   | `ADBMediaTypeVideo` | Tipo di supporto per i flussi video. |

   Il formato generale per la creazione di `MediaObject`:

   ```
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME>
                                          mediaId:<MEDIA_ID>
                                           length:<MEDIA_LENGTH>                       
                                       streamType:<STREAM_TYPE>
                                        mediaType: <MEDIA_TYPE>];
   ```

1. **Allegare metadati video**

   Facoltativamente, allega oggetti metadati video standard e/o personalizzati alla sessione di tracciamento video attraverso variabili di dati di contesto.

   * **Metadati video standard**

      * [Implementazione dei metadati standard su iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **Tasti di metadati video**

         [Chiavi dei metadati iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * Vedi l&#39;elenco completo dei metadati video qui: [Parametri audio e video](/help/metrics-and-metadata/audio-video-parameters.md)
      >[!NOTE]
      >
      >Il collegamento dell&#39;oggetto metadati video standard all&#39;oggetto multimediale è facoltativo.

   * **Metadati personalizzati**

      Crea un oggetto variabile per le variabili personalizzate e inserisci i dati del video. Ad esempio:

      ```
      NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
      [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
      [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
      ```


1. **Tracciare l&#39;intenzione di avviare la riproduzione**

   Per iniziare a monitorare una sessione multimediale, chiama `trackSessionStart` sull&#39;istanza Media Heartbeat.

   >[!TIP]
   >
   >Il secondo valore è il nome dell&#39;oggetto metadati video personalizzato creato al passaggio 2.

   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification {
   //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil];
       [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata];
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` tiene traccia delle intenzioni dell&#39;utente in merito alla riproduzione, non dell&#39;inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati video e per stimare la metrica QoS time-to-start (la durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzi metadati video personalizzati, invia semplicemente un oggetto vuoto per l’argomento `data` in `trackSessionStart`, come mostrato nella riga commento nell’esempio iOS precedente.

1. **Tracciare l&#39;inizio effettivo della riproduzione**

   Identifica l’evento dal lettore video per l’inizio della riproduzione del video, in cui viene eseguito il rendering del primo fotogramma del video sullo schermo, e chiama `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

1. **Tracciare il completamento della riproduzione**

   Identifica l’evento dal lettore video per il completamento della riproduzione video, in cui l’utente ha guardato il contenuto fino alla fine, e chiama `trackComplete`:

   ```
   - (void)onVideoComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackComplete];
   }
   ```

1. **Monitora la fine della sessione**

   Identifica l’evento dal lettore video per lo scaricamento/la chiusura della riproduzione video, in cui l’utente chiude il video e/o il video viene completato e scaricato, e chiama `trackSessionEnd`:

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification {
       [_mediaHeartbeat trackSessionEnd];
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` segna la fine di una sessione di tracciamento video. Se la sessione è stata controllata correttamente al completamento, dove l’utente ha guardato il contenuto fino alla fine, assicurati che `trackComplete` venga chiamato prima di `trackSessionEnd`. Qualsiasi altra chiamata API `track*` viene ignorata dopo `trackSessionEnd`, tranne `trackSessionStart` per una nuova sessione di tracciamento video.

1. **Tracciare tutti gli scenari di pausa possibili**

   Identifica l&#39;evento dal lettore video per la pausa video e chiama `trackPause`:

   ```
   - (void)onVideoPause:(NSNotification *)notification {
       [_mediaHeartbeat trackPause];
   }
   ```

   **Pausa scenari**

   Identifica qualsiasi scenario in cui il lettore video verrà messo in pausa e assicurati che `trackPause` sia chiamato correttamente. I seguenti scenari richiedono tutti che la chiamata all&#39;app `trackPause()`:

   * L’utente inserisce esplicitamente una pausa nell’app.
   * Il lettore si mette in stato di Pausa.
   * (*App mobili*) - L&#39;utente mette l&#39;applicazione in background, ma desideri che l&#39;app mantenga aperta la sessione.
   * (*App mobili*) - Si verifica un qualsiasi tipo di interruzione del sistema che causa lo sfondo di un&#39;applicazione. Ad esempio, l’utente riceve una chiamata, o si verifica un pop-up da un’altra applicazione, ma si desidera che l’applicazione mantenga in vita la sessione per dare all’utente la possibilità di riprendere il video dal punto di interruzione.

1. Identifica l&#39;evento dal lettore per la riproduzione video e/o la ripresa video dalla pausa e chiama `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

   >[!TIP]
   >
   >Può trattarsi della stessa origine evento utilizzata nel passaggio 4. Assicurati che ogni `trackPause()` chiamata API sia associata a una seguente chiamata `trackPlay()` API quando la riproduzione video riprende.

Per ulteriori informazioni sul tracciamento della riproduzione core, consulta quanto segue:

* Scenari di tracciamento: [Riproduzione VOD senza annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Esempio di lettore incluso con l&#39;SDK iOS per un esempio di tracciamento completo.
