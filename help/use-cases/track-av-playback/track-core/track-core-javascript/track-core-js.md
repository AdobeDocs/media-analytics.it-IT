---
title: Scopri come tracciare la riproduzione di base utilizzando JavaScript 2.x
description: Scopri come implementare il tracciamento di base utilizzando Media SDK in un browser che utilizza le app JavaScript 2.x.
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab
exl-id: d8af37a0-9048-4e6b-8cba-809386cbed5f
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Tracciare la riproduzione di base in JavaScript 2.x {#track-core-playback-on-javascript}

Le istruzioni seguenti forniscono indicazioni per l’implementazione negli SDK 2.x.

>[!IMPORTANT]
>Se stai implementando una versione 1.x di SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK](/help/getting-started/download-sdks.md)

1. **Configurazione del tracciamento iniziale**

   Identifica quando l’utente attiva l’intenzione di riproduzione (l’utente fa clic su play e/o l’esecuzione automatica è attiva) e crea un’istanza `MediaObject`.

   [API createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nome variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome file multimediale | Sì |
   | `mediaid` | Identificatore univoco del file multimediale | Sì |
   | `length` | Lunghezza del file multimediale | Sì |
   | `streamType` | Tipo di flusso (vedi _Costanti StreamType_ sotto) | Sì |
   | `mediaType` | Tipo di file multimediale (vedi _Costanti MediaType_ sotto) | Sì |

   **`StreamType`Costanti:**

   | Nome costante | Descrizione   |
   |---|---|
   | `VOD` | Tipo di flusso per Video on Demand. |
   | `LIVE` | Tipo di flusso per il contenuto LIVE. |
   | `LINEAR` | Tipo di flusso per contenuti LINEAR. |
   | `AOD` | Tipo di flusso per audio on-demand. |
   | `AUDIOBOOK` | Tipo di flusso per audiolibro. |
   | `PODCAST` | Tipo di flusso per podcast. |

   Costanti **`MediaType`:**

   | Nome costante | Descrizione |
   |---|---|
   | `Audio` | Tipo di file multimediale per flussi Audio. |
   | `Video` | Tipo di file multimediale per i flussi Video. |

   ```
   var mediaObject =  
     MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,
                                     MediaHeartbeat.StreamType.VOD,
                                     <MEDIA_TYPE>);
   ```

1. **Allega metadati**

   Facoltativamente, allega oggetti metadati standard e/o personalizzati alla sessione di tracciamento tramite variabili di dati di contesto.

   * **Metadati standard**

     [Implementazione dei metadati standard in JavaScript](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)

     >[!NOTE]
     >
     >Il collegamento dell’oggetto metadati standard all’oggetto multimediale è facoltativo.

      * Riferimento API per le chiavi di metadati multimediali: [Chiavi di metadati standard - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

        Consulta il set completo dei metadati disponibili qui: [Parametri audio e video](/help/implementation/variables/audio-video-parameters.md)

   * **Metadati personalizzati**

     Crea un oggetto variabile per le variabili personalizzate e compila i dati per questo elemento multimediale. Ad esempio:

     ```js
     /* Set custom context data */
     var customVideoMetadata = {
         isUserLoggedIn: "false",
         tvStation: "Sample TV station",
         programmer: "Sample programmer"
     };
     ```

1. **Tracciare l’intenzione di inizio riproduzione**

   Per iniziare a tracciare una sessione multimediale, effettua una chiamata `trackSessionStart` sull’istanza Media Heartbeat:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >Il secondo valore è il nome dell’oggetto metadati multimediali personalizzati creato al passaggio 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` tiene traccia delle intenzioni di riproduzione dell’utente, non dell’inizio della riproduzione. Questa API viene utilizzata per caricare dati/metadati e per stimare la metrica QoS relativa al tempo di avvio (durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzi metadati personalizzati, invia semplicemente un oggetto vuoto per l’argomento `data` in `trackSessionStart`, come mostrato nella riga esterna di commento nell’esempio di iOS precedente.

1. **Tracciare l’inizio effettivo della riproduzione**

   Identifica l’evento dal lettore multimediale per l’inizio della riproduzione, dove viene eseguito il rendering del primo fotogramma del file multimediale sullo schermo ed effettua una chiamata `trackPlay`.

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Tracciare il completamento della riproduzione**

   Identifica l’evento dal lettore multimediale per il completamento della riproduzione in cui l’utente ha guardato il contenuto fino alla fine ed effettua una chiamata `trackComplete`.

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Tracciare la fine della sessione**

   Identifica l’evento dal lettore multimediale per lo scaricamento/la chiusura della riproduzione in cui l’utente chiude l’elemento multimediale e/o l’elemento multimediale viene completato e scaricato ed effettua una chiamata `trackSessionEnd`.

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` indica la fine di una sessione di tracciamento. Se la sessione è stata guardata correttamente fino al completamento, dove l’utente ha guardato il contenuto fino alla fine, assicurati che `trackComplete` venga chiamato prima di `trackSessionEnd`. Dopo `trackSessionEnd`, qualsiasi chiamata API `track*` viene ignorata, tranne la chiamata `trackSessionStart` per una nuova sessione di tracciamento video.

1. **Tracciare tutti gli scenari di pausa possibili**

   Identifica l’evento dal lettore multimediale per la pausa ed effettua una chiamata `trackPause`.

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Scenari di pausa**

   Identifica uno scenario in cui il lettore multimediale si interrompe e verifica che `trackPause` sia chiamato correttamente. I seguenti scenari richiedono tutti una chiamata `trackPause()` dall’app:

   * L’utente mette esplicitamente in pausa l’app.
   * Il lettore si mette in pausa da solo.
   * (*App per dispositivi mobili*): l’utente mette l’applicazione in background, ma si desidera invece che l’app mantenga aperta la sessione.
   * (*App per dispositivi mobili*) - Può verificarsi qualsiasi tipo di interruzione di sistema che porta l’applicazione in background. Ad esempio, l’utente riceve una chiamata oppure la notifica da un’altra applicazione, ma desideri che l’applicazione mantenga aperta la sessione per dare all’utente l’opportunità di riprendere l’elemento multimediale dal punto in cui è stato interrotto.

1. Identifica l’evento dal lettore per la riproduzione e/o la ripresa dalla pausa ed effettua una chiamata `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >Potrebbe trattarsi della stessa origine evento utilizzata nel passaggio 4. Quando la riproduzione riprende, assicurati che ogni chiamata API `trackPause()` sia associata alla seguente chiamata API `trackPlay()`.

* Scenari di tracciamento: [Riproduzione VOD senza annunci](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso con l’SDK JavaScript per un esempio di tracciamento completo.
