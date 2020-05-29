---
title: Tenere traccia della riproduzione di base mediante JavaScript v3.x
description: Questo argomento descrive come implementare il tracciamento di base utilizzando Media SDK in un browser utilizzando le app JavaScript 3.x.
translation-type: tm+mt
source-git-commit: 40d75ef32596e915ac07c173b4595bb78db3688d
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 2%

---


# Tenere traccia della riproduzione di base mediante JavaScript 3.x{#track-core-playback-on-javascript}

>[!IMPORTANT]
>Questa documentazione descrive il tracciamento nella versione 3.x dell’SDK. Se stai implementando versioni precedenti dell’SDK, puoi scaricare le Guide per gli sviluppatori qui: [Download di SDK](/help/sdk-implement/download-sdks.md)

1. **Configurazione iniziale tracciamento**

   Identificare quando l&#39;utente attiva l&#39;intenzione di riproduzione (l&#39;utente fa clic su play e/o la riproduzione automatica è attivata) e creare un&#39; `MediaObject` istanza.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nome della variabile | Tipo | Descrizione |
   | --- | --- | --- |
   | `name` | string | Stringa non vuota che denota il nome del supporto. |
   | `id` | string | Stringa non vuota che denota un unico identificatore multimediale. |
   | `length` | number | Numero positivo che indica la lunghezza del supporto in secondi. Utilizzate 0 se la lunghezza è sconosciuta. |
   | `streamType` | string |  |
   | `mediaType` |  | Tipo di supporto (Audio o Video). |

   **`StreamType`costanti:**

   | Nome costante | Descrizione   |
   |---|---|
   | `VOD` | Tipo di flusso per Video on Demand. |
   | `AOD` | Tipo di flusso per Audio su richiesta. |

   **`MediaType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `Audio` | Tipo di supporto per i flussi audio. |
   | `Video` | Tipo di supporto per i flussi video. |

   ```
   var mediaObject = ADB.Media.createMediaObject(<MEDIA_NAME>,
                                     <MEDIA_ID,
                                     <MEDIA_LENGTH>,
                                     <STREAM_TYPE>,
                                     <MEDIA_TYPE>);
   ```

1. **Allega metadati**

   Se necessario, allegate metadati standard e/o personalizzati alla sessione di tracciamento tramite variabili di dati di contesto.

   * **Metadati standard**

      >[!NOTE]
      >
      >È possibile allegare i metadati standard.

      * Riferimento API per le chiavi di metadati multimediali - chiavi di metadati [standard - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         Consultate il set completo dei metadati disponibili qui: [Parametri audio e video](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Metadati personalizzati**

      Create un oggetto variabile per le variabili personalizzate e inserite i dati per questo supporto. Ad esempio:

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


1. **Tenere traccia dell’intenzione di avviare la riproduzione**

   Per avviare il tracciamento di una sessione multimediale, invocate `trackSessionStart` l’istanza Media Heartbeat:

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
   >`trackSessionStart` tiene traccia delle intenzioni dell’utente in merito alla riproduzione, non dell’inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati e per stimare la metrica QoS time-to-start (la durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non si utilizza contextData, è sufficiente inviare un oggetto vuoto per l&#39; `data` argomento in `trackSessionStart`.

1. **Tracciare l’inizio effettivo della riproduzione**

   Identificate l’evento dal lettore multimediale per l’inizio della riproduzione, dove viene riprodotto il primo fotogramma del file multimediale sullo schermo, e chiamate `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

1. **Tenere traccia del completamento della riproduzione**

   Identificate l’evento dal lettore multimediale per il completamento della riproduzione, in cui l’utente ha guardato il contenuto fino alla fine, e chiamate `trackComplete`:

   ```js
   tracker.trackComplete();
   ```

1. **Tenere traccia della fine della sessione**

   Identificare l’evento dal lettore multimediale per lo scaricamento/la chiusura della riproduzione, in cui l’utente chiude il supporto e/o il supporto è stato completato e scaricato, e chiamare `trackSessionEnd`:

   ```js
   tracker.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` segna la fine di una sessione di tracciamento. Se la sessione è stata guardata con successo e l’utente ha guardato il contenuto fino alla fine, accertatevi che `trackComplete` venga chiamato prima `trackSessionEnd`. Qualsiasi altra chiamata `track*` API viene ignorata dopo `trackSessionEnd`, fatta eccezione per `trackSessionStart` una nuova sessione di tracciamento.

1. **Tenere traccia di tutti gli scenari di pausa possibili**

   Identificare l’evento dal lettore multimediale per la pausa e la chiamata `trackPause`:

   ```js
   tracker.trackPause();
   ```

   **Pausa scenari**

   Identificare qualsiasi scenario in cui il lettore multimediale si mette in pausa e assicurarsi che venga chiamato `trackPause` correttamente. Tutti gli scenari seguenti richiedono che la chiamata dell&#39;app `trackPause()`:

   * L&#39;utente interrompe esplicitamente la pausa nell&#39;app.
   * Il lettore si mette nello stato Pausa.
   * (App *mobili*) - L&#39;utente mette l&#39;applicazione in background, ma si desidera che l&#39;app tenga aperta la sessione.
   * (App *mobili*) - Si verifica qualsiasi tipo di interruzione del sistema che causa il background di un&#39;applicazione. Ad esempio, l&#39;utente riceve una chiamata, o si verifica un pop-up da un&#39;altra applicazione, ma si desidera che l&#39;applicazione mantenga in vita la sessione per dare all&#39;utente la possibilità di riprendere il supporto dal punto di interruzione.

1. Identificare l’evento dal lettore per la riproduzione e/o la ripresa dalla pausa e dalla chiamata `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

   >[!TIP]
   >
   >Può trattarsi della stessa origine evento utilizzata nel passaggio 4. Assicurati che ogni chiamata `trackPause()` API sia associata a una chiamata `trackPlay()` API seguente quando la riproduzione riprende.

* Scenari di tracciamento: [Riproduzione VOD senza annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso con l’SDK JavaScript per un esempio di tracciamento completo.
