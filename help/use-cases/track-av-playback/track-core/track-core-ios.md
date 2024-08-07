---
title: Scopri come tracciare la riproduzione di base in iOS
description: Scopri come implementare il tracciamento di base utilizzando Media SDK su iOS.
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
exl-id: 5c6b36b3-a421-45a4-a65e-4eb57513ca4a
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: c308dba2d7cf07b89bf124bd6e5f972c253c9f18
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 100%

---

# Tracciare la riproduzione di base su iOS {#track-core-playback-on-ios}

Questa documentazione tratta il tracciamento nella versione 2.x dell’SDK.

>[!IMPORTANT]
>
>Se stai implementando una versione 1.x di SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK](/help/getting-started/download-sdks.md)

1. **Configurazione del tracciamento iniziale**

   Identifica quando l’utente attiva l’intenzione di riproduzione (l’utente fa clic su play e/o l’esecuzione automatica è attiva) e crea un’istanza `MediaObject`.

   [API createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | Nome variabile | Descrizione | Obbligatorio |
   |---|---|---|
   | `name` | Nome del video | Sì |
   | `mediaid` | Identificatore univoco del video | Sì |
   | `length` | Lunghezza video | Sì |
   | `streamType` | Tipo di flusso (vedi _Costanti StreamType_ sotto) | Sì |
   | `mediaType` | Tipo di file multimediale (vedi _Costanti MediaType_ sotto) | Sì |

   **`StreamType`Costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | Tipo di flusso per video on demand |
   | `ADBMediaHeartbeatStreamTypeLIVE` | Tipo di flusso per il contenuto live |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | Tipo di flusso per il contenuto lineare |
   | `ADBMediaHeartbeatStreamTypeAOD` | Tipo di flusso per audio on-demand |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | Tipo di flusso per audiolibro |
   | `ADBMediaHeartbeatStreamTypePODCAST` | Tipo di flusso per Podcast |

   **`MediaType`Costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `ADBMediaTypeAudio` | Tipo di file multimediale per flussi Audio. |
   | `ADBMediaTypeVideo` | Tipo di file multimediale per i flussi Video. |

   Il formato generale per la creazione del `MediaObject`:

   ```
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME>
                                          mediaId:<MEDIA_ID>
                                           length:<MEDIA_LENGTH>                       
                                       streamType:<STREAM_TYPE>
                                        mediaType: <MEDIA_TYPE>];
   ```

1. **Allegare metadati video**

   Facoltativamente, puoi allegare oggetti metadati video standard e/o personalizzati alla sessione di tracciamento video attraverso variabili dei dati di contesto.

   * **Metadati video standard**

      * [Implementare metadati standard su iOS](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **Chiavi metadati video**
        [Chiavi metadati iOS](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * Consulta l’elenco completo dei metadati video qui: [Parametri audio e video](/help/implementation/variables/audio-video-parameters.md)

     >[!NOTE]
     >
     >Il collegamento dell’oggetto metadati video standard all’oggetto multimediale è facoltativo.

   * **Metadati personalizzati**

     Crea un oggetto variabile per le variabili personalizzate e lo popola con i dati del video. Ad esempio:

     ```
     NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
     [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
     [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
     ```

1. **Tracciare l’intenzione di avviare la riproduzione**

   Per iniziare a tracciare una sessione multimediale, effettua una chiamata `trackSessionStart` sull’istanza Media Heartbit.

   >[!TIP]
   >
   >Il secondo valore corrisponde al nome dell’oggetto metadati video personalizzato creato nel passaggio 2.

   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification {
   //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil];
       [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata];
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` tiene traccia delle intenzioni dell’utente in merito alla riproduzione, non dell’inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati video e per stimare la metrica QoS relativa al tempo di avvio (durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzi metadati video personalizzati, invia semplicemente un oggetto vuoto per l’argomento `data` in `trackSessionStart`, come mostrato nella riga esterna di commento nell’esempio di iOS precedente.

1. **Tracciare l’inizio effettivo della riproduzione**

   Identifica l’evento dal lettore video per l’inizio della riproduzione, in cui viene eseguito il rendering del primo fotogramma del video sullo schermo ed effettua una chiamata `trackPlay`.

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

1. **Tracciare il completamento della riproduzione**

   Identifica l’evento dal lettore video per il completamento della riproduzione, in cui l’utente ha guardato il contenuto fino alla fine, ed effettua una chiamata `trackComplete`.

   ```
   - (void)onVideoComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackComplete];
   }
   ```

1. **Tracciamento della fine della sessione**

   Identifica l’evento dal lettore video per lo scaricamento/la chiusura della riproduzione, in cui l’utente chiude il video e/o il video viene completato e scaricato, quindi effettua una chiamata `trackSessionEnd`.

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification {
       [_mediaHeartbeat trackSessionEnd];
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` indica la fine di una sessione di tracciamento video. Se la sessione è stata vista correttamente fino al completamento, per cui l’utente ha guardato il contenuto fino alla fine, assicurati che `trackComplete` venga chiamato prima di `trackSessionEnd`. Dopo `trackSessionEnd`, qualsiasi chiamata API `track*` viene ignorata, tranne che la chiamata `trackSessionStart` per una nuova sessione di tracciamento video.

1. **Tracciare tutti gli scenari di pausa possibili**

   Identifica l’evento dal lettore video per la pausa video e la chiamata `trackPause`:

   ```
   - (void)onVideoPause:(NSNotification *)notification {
       [_mediaHeartbeat trackPause];
   }
   ```

   **Scenari di pausa**

   Identifica uno scenario in cui il lettore video si interrompe e verifica che `trackPause` sia chiamato correttamente. I seguenti scenari richiedono tutti una chiamata `trackPause()` dall’app:

   * L’utente mette esplicitamente in pausa l’app.
   * Il lettore si mette in pausa da solo.
   * (*App per dispositivi mobili*): l’utente mette l’applicazione in background, ma si desidera invece che l’app mantenga aperta la sessione.
   * (*App per dispositivi mobili*): si verifica una qualsiasi interruzione del sistema causando l’esecuzione in background dell’applicazione. Ad esempio, l’utente riceve una chiamata oppure la notifica da un’altra applicazione, ma desideri che l’applicazione mantenga aperta la sessione per dare all’utente l’opportunità di riprendere il video dal punto in cui è stato interrotto.

1. Identifica l’evento dal lettore per la riproduzione video e/o la ripresa del video dalla pausa ed effettua una chiamata `trackPlay`.

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

   >[!TIP]
   >
   >Potrebbe trattarsi della stessa origine evento utilizzata nel passaggio 4. Assicurati che ogni chiamata API `trackPause()` sia associata alla successiva chiamata API `trackPlay()` quando la riproduzione video riprende.

Per ulteriori informazioni sul tracciamento della riproduzione core, consulta:

* Scenari di tracciamento: [Riproduzione VOD senza annunci](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso nell’SDK per iOS, con un esempio di tracciamento completo.
