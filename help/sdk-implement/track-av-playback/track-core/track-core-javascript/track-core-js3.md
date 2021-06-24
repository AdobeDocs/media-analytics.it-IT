---
title: Scopri come tenere traccia della riproduzione core utilizzando JavaScript v3.x
description: Scopri come implementare il tracciamento di base utilizzando Media SDK in un browser utilizzando le app JavaScript 3.x.
exl-id: f3145450-82ba-4790-91a4-9d2cc97bbaa5
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 2%

---

# Tracciamento riproduzione core con JavaScript 3.x{#track-core-playback-on-javascript}

>[!IMPORTANT]
>Questa documentazione tratta il tracciamento nella versione 3.x dell&#39;SDK. Se implementi una versione precedente dell’SDK, puoi scaricare le Guide per sviluppatori qui: [Scaricare gli SDK](/help/sdk-implement/download-sdks.md)

1. **Configurazione del tracciamento iniziale**

   Identifica quando l&#39;utente attiva l&#39;intenzione di riproduzione (l&#39;utente fa clic su play e/o autoplay è attivato) e crea un&#39;istanza `MediaObject`.

   [API createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nome variable | Tipo | Descrizione |
   | --- | --- | --- |
   | `name` | string | Stringa non vuota che indica il nome del supporto. |
   | `id` | string | Stringa non vuota che indica un identificatore di supporto univoco. |
   | `length` | numero | Numero positivo che indica la lunghezza del supporto in secondi. Utilizzare 0 se la lunghezza è sconosciuta. |
   | `streamType` | string |  |
   | `mediaType` |  | Tipo di supporto (audio o video). |

   **`StreamType`costanti:**

   | Nome costante | Descrizione   |
   |---|---|
   | `VOD` | Tipo di flusso per Video on Demand. |
   | `AOD` | Tipo di flusso per Audio on Demand. |

   **`MediaType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `Audio` | Tipo di supporto per flussi audio. |
   | `Video` | Tipo di supporto per i flussi video. |

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
      >L&#39;aggiunta dei metadati standard è facoltativa.

      * Riferimento API per le chiavi dei metadati multimediali - [chiavi dei metadati standard - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         Vedi il set completo dei metadati disponibili qui: [Parametri audio e video](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Metadati personalizzati**

      Crea un oggetto variabile per le variabili personalizzate e compila i dati per questo supporto. Ad esempio:

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


1. **Tracciare l&#39;intenzione di avviare la riproduzione**

   Per iniziare a monitorare una sessione multimediale, chiama `trackSessionStart` sull&#39;istanza Media Heartbeat:

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
   >`trackSessionStart` tiene traccia delle intenzioni dell&#39;utente in merito alla riproduzione, non dell&#39;inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati e per stimare la metrica QoS time-to-start (la durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzi contextData, invia semplicemente un oggetto vuoto per l&#39;argomento `data` in `trackSessionStart`.

1. **Tracciare l&#39;inizio effettivo della riproduzione**

   Identificare l&#39;evento dal lettore multimediale per l&#39;inizio della riproduzione, dove viene eseguito il rendering del primo fotogramma del file multimediale sullo schermo, e chiamare `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

1. **Tracciare il completamento della riproduzione**

   Identificare l&#39;evento dal lettore multimediale per il completamento della riproduzione, dove l&#39;utente ha guardato il contenuto fino alla fine, e chiamare `trackComplete`:

   ```js
   tracker.trackComplete();
   ```

1. **Monitora la fine della sessione**

   Identificare l&#39;evento dal lettore multimediale per lo scaricamento/la chiusura della riproduzione, in cui l&#39;utente chiude il supporto e/o il supporto è stato completato e scaricato, e chiamare `trackSessionEnd`:

   ```js
   tracker.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` segna la fine di una sessione di tracciamento. Se la sessione è stata controllata correttamente al completamento, dove l’utente ha guardato il contenuto fino alla fine, assicurati che `trackComplete` venga chiamato prima di `trackSessionEnd`. Qualsiasi altra chiamata API `track*` viene ignorata dopo `trackSessionEnd`, tranne `trackSessionStart` per una nuova sessione di tracciamento.

1. **Tracciare tutti gli scenari di pausa possibili**

   Identifica l&#39;evento dal lettore multimediale per la pausa e la chiamata `trackPause`:

   ```js
   tracker.trackPause();
   ```

   **Pausa scenari**

   Identifica qualsiasi scenario in cui il lettore multimediale si mette in pausa e assicurati che `trackPause` sia chiamato correttamente. I seguenti scenari richiedono tutti che la chiamata all&#39;app `trackPause()`:

   * L’utente inserisce esplicitamente una pausa nell’app.
   * Il lettore si mette in stato di Pausa.
   * (*App mobili*) - L&#39;utente mette l&#39;applicazione in background, ma desideri che l&#39;app mantenga aperta la sessione.
   * (*App mobili*) - Si verifica un qualsiasi tipo di interruzione del sistema che causa lo sfondo di un&#39;applicazione. Ad esempio, l&#39;utente riceve una chiamata, o si verifica un pop-up da un&#39;altra applicazione, ma si desidera che l&#39;applicazione mantenga in vita la sessione per dare all&#39;utente la possibilità di riprendere il supporto dal punto di interruzione.

1. Identifica l&#39;evento dal lettore per la riproduzione e/o la ripresa dalla pausa e chiama `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

   >[!TIP]
   >
   >Può trattarsi della stessa origine evento utilizzata nel passaggio 4. Assicurati che ogni chiamata API `trackPause()` sia associata a una seguente chiamata API `trackPlay()` quando la riproduzione riprende.

* Scenari di tracciamento: [Riproduzione VOD senza annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso nell&#39;SDK JavaScript per un esempio di tracciamento completo.
