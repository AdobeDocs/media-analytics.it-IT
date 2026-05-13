---
title: Scopri come tracciare la riproduzione di base in iOS
description: Scopri come implementare il tracciamento di base utilizzando Media SDK su iOS.
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
exl-id: 5c6b36b3-a421-45a4-a65e-4eb57513ca4a
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/M-BlP6PGMAzyieFg3QDJTBcKE-Tw2PFCoNlB6G1E3KI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 707
ht-degree: 99%

---

# Tracciare la riproduzione di base su iOS{#track-core-playback-on-ios}

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

1. **Tracciare l’intenzione di inizio riproduzione**

   Per iniziare a tracciare una sessione multimediale, chiama `trackSessionStart` sull’istanza Media Heartbeat.

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
   >`trackSessionStart` tiene traccia delle intenzioni di riproduzione dell’utente, non dell’inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati video e per stimare la metrica QoS relativa al tempo di avvio (durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzi metadati video personalizzati, invia semplicemente un oggetto vuoto per l’argomento `data` in `trackSessionStart`, come mostrato nella riga esterna di commento nell’esempio di iOS precedente.

1. **Tracciare l’inizio effettivo della riproduzione**

   Identifica l’evento dal lettore video per l’inizio della riproduzione, in cui viene eseguito il rendering del primo fotogramma del video sullo schermo, quindi effettua una chiamata `trackPlay`.

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

   Identifica uno scenario in cui il lettore video si interrompe e verifica che `trackPause` sia chiamato correttamente. Tutti gli scenari seguenti richiedono che l’app chiami `trackPause()`:

   * L’utente mette esplicitamente in pausa l’app.
   * Il lettore si mette in pausa da solo.
   * (*App per dispositivi mobili*): l’utente mette l’applicazione in background, ma si desidera invece che l’app mantenga aperta la sessione.
   * (*App mobili*): si verifica una qualsiasi interruzione del sistema causando l’esecuzione in background dell’applicazione. Ad esempio, l’utente riceve una chiamata oppure la notifica da un’altra applicazione, ma desideri che l’applicazione mantenga aperta la sessione per dare all’utente l’opportunità di riprendere il video dal punto in cui è stato interrotto.

1. Identifica l’evento dal lettore per la riproduzione video e/o la ripresa del video dalla pausa ed effettua una chiamata `trackPlay`.

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

   >[!TIP]
   >
   >Potrebbe trattarsi della stessa origine evento utilizzata nel passaggio 4. Quando la riproduzione del video riprende, assicurati che ogni chiamata API `trackPause()` sia associata alla seguente chiamata API `trackPlay()`.

Per ulteriori informazioni sul tracciamento della riproduzione core, consulta:

* Scenari di tracciamento: [riproduzione VOD senza annunci](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso nell’SDK per iOS, con un esempio di tracciamento completo.
