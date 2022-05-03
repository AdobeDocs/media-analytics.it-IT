---
title: Scopri come tenere traccia della riproduzione core utilizzando JavaScript v3.x
description: Scopri come implementare il tracciamento di base utilizzando Media SDK in un browser utilizzando le app JavaScript 3.x.
exl-id: f3145450-82ba-4790-91a4-9d2cc97bbaa5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: ht
source-wordcount: '645'
ht-degree: 100%

---

# Tracciare la riproduzione di base in JavaScript 3.x {#track-core-playback-on-javascript}

Questa documentazione tratta il tracciamento nella versione 3.x dell’SDK.

>[!IMPORTANT]
> Se implementi una versione precedente dell’SDK, puoi scaricare le Guide per sviluppatori qui: [Scaricare gli SDK](/help/sdk-implement/download-sdks.md)

1. **Configurazione del tracciamento iniziale**

   Identifica quando l’utente attiva l’intenzione di riproduzione (l’utente fa clic su play e/o l’esecuzione automatica è attiva) e crea un’istanza `MediaObject`.

   [API createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nome variabile | Tipo | Descrizione |
   | --- | --- | --- |
   | `name` | stringa | Stringa non vuota che indica il nome del file multimediale. |
   | `id` | stringa | Stringa non vuota che indica un identificatore del file multimediale univoco. |
   | `length` | numero | Numero positivo che indica la lunghezza del file multimediale in secondi. Usa 0 se la lunghezza è sconosciuta. |
   | `streamType` | stringa |  |
   | `mediaType` |  | Tipo di file multimediale (audio o video). |

   Costanti **`StreamType`:**

   | Nome costante | Descrizione   |
   |---|---|
   | `VOD` | Tipo di flusso per Video on Demand. |
   | `AOD` | Tipo di flusso per audio on-demand. |

   Costanti **`MediaType`:**

   | Nome costante | Descrizione |
   |---|---|
   | `Audio` | Tipo di file multimediale per flussi Audio. |
   | `Video` | Tipo di file multimediale per i flussi Video. |

   ```
   var mediaObject = ADB.Media.createMediaObject(<MEDIA_NAME>,
                                     <MEDIA_ID,
                                     <MEDIA_LENGTH>,
                                     <STREAM_TYPE>,
                                     <MEDIA_TYPE>);
   ```

1. **Allega metadati**

   Facoltativamente, allega metadati standard e/o personalizzati alla sessione di tracciamento tramite variabili di dati di contesto.

   * **Metadati standard**

      >[!NOTE]
      >
      >L’aggiunta dei metadati standard è facoltativa.

      * Riferimento API per le chiavi di metadati multimediali - [Chiavi di metadati standard - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         Vedi il set completo dei metadati disponibili qui: [Parametri audio e video](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Metadati personalizzati**

      Crea un oggetto variabile per le variabili personalizzate e compila i dati per questo elemento multimediale. Ad esempio:

      ```js
      /* Set context data */
       var contextData = {};
      
       //Standard metadata
       contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
       contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
      
       //Custom metadata
       contextData["isUserLoggedIn"] = "false";
       contextData["tvStation"] = "Sample TV Station";
      ```


1. **Tracciare l’intenzione di avviare la riproduzione**

   Per iniziare a tracciare una sessione multimediale, chiama `trackSessionStart` sull’istanza Media Heartbeat:

   ```js
   var mediaObject = ADB.Media.createMediaObject("video-name",
                                                 "video-id",
                                                 60.0,
                                                 ADB.Media.StreamType.VOD,
                                                 ADB.Media.MediaType.Video);
   
   var contextData = {};
   
   //Standard metadata
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
   
   //Custom metadata
   contextData["isUserLoggedIn"] = "false";
   contextData["tvStation"] = "Sample TV Station";
   
   tracker.trackSessionStart(mediaObject, contextData);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` tiene traccia delle intenzioni di riproduzione dell’utente, non dell’inizio della riproduzione. Questa API viene utilizzata per caricare dati/metadati e per stimare la metrica QoS relativa al tempo di avvio (durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzi contextData, invia semplicemente un oggetto vuoto per l’argomento `data` in `trackSessionStart`.

1. **Tracciare l’inizio effettivo della riproduzione**

   Identifica l’evento dal lettore multimediale per l’inizio della riproduzione, dove viene eseguito il rendering del primo fotogramma del file multimediale sullo schermo, e chiama `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

1. **Tracciare il completamento della riproduzione**

   Identifica l’evento dal lettore multimediale per il completamento della riproduzione dove l’utente ha guardato il contenuto fino alla fine e chiama `trackComplete`:

   ```js
   tracker.trackComplete();
   ```

1. **Monitorare la fine della sessione**

   Identifica l’evento dal lettore multimediale per lo scaricamento/la chiusura della riproduzione in cui l’utente chiude il file multimediale e/o il file multimediale è stato completato e scaricato e chiama `trackSessionEnd`:

   ```js
   tracker.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` segna la fine di una sessione di tracciamento. Se la sessione è stata controllata correttamente al completamento, dove l’utente ha guardato il contenuto fino alla fine, assicurati che `trackComplete` venga chiamato prima di `trackSessionEnd`. Qualsiasi altra chiamata API `track*` viene ignorata dopo `trackSessionEnd`, tranne `trackSessionStart` per una nuova sessione di tracciamento.

1. **Tracciare tutti gli scenari di pausa possibili**

   Identifica l’evento dal lettore multimediale per la pausa e chiama `trackPause`:

   ```js
   tracker.trackPause();
   ```

   **Scenari di pausa**

   Identifica uno scenario in cui il lettore multimediale si mette in pausa e assicurati che `trackPause` venga chiamato correttamente. I seguenti scenari richiedono tutti una chiamata all’app `trackPause()`:

   * L’utente mette esplicitamente in pausa l’app.
   * Il lettore si mette in pausa da solo.
   * (*App per dispositivi mobili*): l’utente mette l’applicazione in background, ma desideri che l’app mantenga aperta la sessione.
   * (*App per dispositivi mobili*): si verifica una qualsiasi interruzione del sistema causando l’esecuzione in background dell’applicazione. Ad esempio, l’utente riceve una chiamata oppure la notifica da un’altra applicazione, ma desideri che l’applicazione mantenga aperta la sessione per dare all’utente l’opportunità di riprendere l’elemento multimediale dal punto in cui è stato interrotto.

1. Identifica l’evento dal lettore per la riproduzione e/o la ripresa dalla pausa e dalla chiamata `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

   >[!TIP]
   >
   >Potrebbe trattarsi della stessa origine evento utilizzata nel passaggio 4. Assicurati che ogni chiamata API `trackPause()` sia associata alla seguente chiamata API `trackPlay()` quando la riproduzione riprende.

* Scenari di tracciamento: [Riproduzione VOD senza annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso con l’SDK JavaScript per un esempio di tracciamento completo.
