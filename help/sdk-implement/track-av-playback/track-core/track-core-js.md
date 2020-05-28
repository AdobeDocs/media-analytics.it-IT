---
title: Tenere traccia della riproduzione di base mediante JavaScript 2.x
description: Questo argomento descrive come implementare il tracciamento di base utilizzando Media SDK in un browser utilizzando le app JavaScript 2.x.
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab
translation-type: tm+mt
source-git-commit: 30ed54924c75a9c33e6122b2d7ddbb84c06b8c0c
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 3%

---


# Tenere traccia della riproduzione di base mediante JavaScript 2.x{#track-core-playback-on-javascript}

>[!IMPORTANT]
>Questa documentazione descrive il tracciamento nella versione 2.x dell’SDK. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Download di SDK](/help/sdk-implement/download-sdks.md)

1. **Configurazione iniziale tracciamento**

   Identificare quando l&#39;utente attiva l&#39;intenzione di riproduzione (l&#39;utente fa clic su play e/o la riproduzione automatica è attivata) e creare un&#39; `MediaObject` istanza.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome file multimediale | Sì |
   | `mediaid` | Identificatore univoco del supporto | Sì |
   | `length` | Lunghezza del supporto | Sì |
   | `streamType` | Tipo di flusso (vedere le costanti __ StreamType riportate di seguito) | Sì |
   | `mediaType` | Tipo di supporto (vedere le costanti __ MediaType riportate di seguito) | Sì |

   **`StreamType`costanti:**

   | Nome costante | Descrizione   |
   |---|---|
   | `VOD` | Tipo di flusso per Video on Demand. |
   | `LIVE` | Tipo di flusso per il contenuto LIVE. |
   | `LINEAR` | Tipo di flusso per il contenuto LINEAR. |
   | `AOD` | Tipo di flusso per Audio su richiesta. |
   | `AUDIOBOOK` | Tipo di flusso per la Rubrica audio. |
   | `PODCAST` | Tipo di flusso per Podcast. |

   **`MediaType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `Audio` | Tipo di supporto per i flussi audio. |
   | `Video` | Tipo di supporto per i flussi video. |

   ```
   var mediaObject =  
     MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,
                                     MediaHeartbeat.StreamType.VOD,
                                     <MEDIA_TYPE>);
   ```

1. **Allega metadati**

   È possibile allegare oggetti metadati standard e/o personalizzati alla sessione di tracciamento tramite variabili di dati di contesto.

   * **Metadati standard**

      [Implementazione dei metadati standard in JavaScript](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >Il collegamento dell&#39;oggetto metadati standard all&#39;oggetto multimediale è facoltativo.

      * Riferimento API per le chiavi di metadati multimediali - chiavi di metadati [standard - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         Consultate il set completo dei metadati disponibili qui: [Parametri audio e video](/help/metrics-and-metadata/audio-video-parameters.md)
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
   >Il secondo valore è il nome dell&#39;oggetto metadati multimediale personalizzato creato al punto 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` tiene traccia delle intenzioni dell’utente in merito alla riproduzione, non dell’inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati e per stimare la metrica QoS time-to-start (la durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzate metadati personalizzati, inviate semplicemente un oggetto vuoto per l&#39; `data` argomento in `trackSessionStart`, come mostrato nella riga commento nell&#39;esempio iOS precedente.

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
   >`trackSessionEnd` segna la fine di una sessione di tracciamento. Se la sessione è stata guardata con successo e l’utente ha guardato il contenuto fino alla fine, accertatevi che `trackComplete` venga chiamato prima `trackSessionEnd`. Qualsiasi altra chiamata `track*` API viene ignorata dopo `trackSessionEnd`, fatta eccezione per `trackSessionStart` una nuova sessione di tracciamento.

1. **Tenere traccia di tutti gli scenari di pausa possibili**

   Identificare l’evento dal lettore multimediale per la pausa e la chiamata `trackPause`:

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Pausa scenari**

   Identificare qualsiasi scenario in cui il lettore multimediale si mette in pausa e assicurarsi che venga chiamato `trackPause` correttamente. Tutti gli scenari seguenti richiedono che la chiamata dell&#39;app `trackPause()`:

   * L&#39;utente interrompe esplicitamente la pausa nell&#39;app.
   * Il lettore si mette nello stato Pausa.
   * (App *mobili*) - L&#39;utente mette l&#39;applicazione in background, ma si desidera che l&#39;app tenga aperta la sessione.
   * (App *mobili*) - Si verifica qualsiasi tipo di interruzione del sistema che causa il background di un&#39;applicazione. Ad esempio, l&#39;utente riceve una chiamata, o si verifica un pop-up da un&#39;altra applicazione, ma si desidera che l&#39;applicazione mantenga in vita la sessione per dare all&#39;utente la possibilità di riprendere il supporto dal punto di interruzione.

1. Identificare l’evento dal lettore per la riproduzione e/o la ripresa dalla pausa e dalla chiamata `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >Può trattarsi della stessa origine evento utilizzata nel passaggio 4. Assicurati che ogni chiamata `trackPause()` API sia associata a una chiamata `trackPlay()` API seguente quando la riproduzione riprende.

* Scenari di tracciamento: [Riproduzione VOD senza annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso con l’SDK JavaScript per un esempio di tracciamento completo.
