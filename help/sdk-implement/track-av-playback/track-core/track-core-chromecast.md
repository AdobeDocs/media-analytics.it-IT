---
title: Tracciare la riproduzione del core su Chromecast
description: In questo argomento viene descritto come implementare il tracciamento di base tramite Media SDK su Chromecast.
uuid: a9fc59d8-a2f4-4889-bdec-55c42a835d06
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Tracciare la riproduzione del core su Chromecast{#track-core-playback-on-chromecast}

>[!IMPORTANT]
>
>Questa documentazione descrive il tracciamento nella versione 2.x dell’SDK. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Download di SDK](/help/sdk-implement/download-sdks.md)

1. **Configurazione iniziale tracciamento**

   Identificare quando l'utente attiva l'intenzione di riproduzione (l'utente fa clic su play e/o la riproduzione automatica è attivata) e creare un' `MediaObject` istanza.

   **`MediaObject`Riferimento API:**

   [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>); 
   ```

   **`StreamType`costanti:**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`costanti:**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **Allega metadati video**

   Facoltativamente, potete allegare oggetti di metadati video standard e/o personalizzati alla sessione di tracciamento video tramite variabili di dati contestuali.

   * **Metadati video standard**

      [Implementazione di metadati standard su Chromecast](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

      >[!NOTE]
      >
      >Il collegamento dell'oggetto di metadati video standard all'oggetto multimediale è facoltativo.

   * **Metadati personalizzati**

      Create un oggetto variabile per le variabili personalizzate e inserite i dati per questo video. Ad esempio:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```

1. **Tenere traccia dell’intenzione di avviare la riproduzione**

   Per iniziare a monitorare una sessione multimediale, invoca [trackSessionStart](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart) sull’ `media` oggetto.

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` tiene traccia delle intenzioni dell’utente in merito alla riproduzione, non dell’inizio della riproduzione. Questa API viene utilizzata per caricare i dati video/metadati e per stimare la metrica QoS time-to-start (la durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Il secondo valore è il nome dell'oggetto di metadati video personalizzato creato al punto 2. Se non utilizzate metadati video personalizzati, inviate semplicemente un oggetto vuoto per l' `data` argomento in `trackSessionStart`, come illustrato nella riga commento nell'esempio iOS precedente.

1. **Tracciare l’inizio effettivo della riproduzione**

   Mediante questo componente, potete identificare l’evento dal lettore video per l’inizio della riproduzione del video, dove viene rappresentato il primo fotogramma del video sullo schermo, e chiamare [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay)

   ```
   ADBMobile.media.trackPlay();
   ```

1. **Tenere traccia del completamento della riproduzione**

   Identificate l’evento dal lettore video per il completamento della riproduzione video, in cui l’utente ha guardato il contenuto fino alla fine, e chiamate [trackComplete:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackComplete();
   ```

1. **Tenere traccia della fine della sessione**

   Mediante questo componente, potete identificare l’evento dal lettore video per lo scaricamento e la chiusura della riproduzione video, in cui l’utente chiude il video e/o il video viene completato e scaricato, e chiamare [trackSessionEnd:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd)

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` segna la fine di una sessione di tracciamento video. Se la sessione è stata guardata con successo e l’utente ha guardato il contenuto fino alla fine, accertatevi che `trackComplete` venga chiamato prima `trackSessionEnd`. Qualsiasi altra chiamata `track*` API viene ignorata dopo `trackSessionEnd`, fatta eccezione per `trackSessionStart` una nuova sessione di tracciamento video.

1. **Tenere traccia di tutti gli scenari di pausa possibili**

   Identificare l’evento dal lettore video per la pausa video e chiamare [trackPause:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause)

   ```
   ADBMobile.media.trackPause();
   ```

   **Pausa scenari**

   Identificate eventuali situazioni in cui il lettore video si interrompe e accertatevi che venga chiamato `trackPause` correttamente. Tutti gli scenari seguenti richiedono che la chiamata dell'app `trackPause()`:

   * L'utente interrompe esplicitamente la pausa nell'app.
   * Il lettore si mette nello stato Pausa.
   * (App *mobili*) - L'utente mette l'applicazione in background, ma si desidera che l'app tenga aperta la sessione.
   * (App *mobili*) - Si verifica qualsiasi tipo di interruzione del sistema che causa il background di un'applicazione. Ad esempio, l'utente riceve una chiamata, o si verifica un pop-up da un'altra applicazione, ma si desidera che l'applicazione mantenga in vita la sessione per dare all'utente la possibilità di riprendere il video dal punto di interruzione.

1. Identificare l’evento dal lettore per la riproduzione video e/o la ripresa video dalla pausa e chiamare [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >Può trattarsi della stessa origine evento utilizzata nel passaggio 4. Quando la riproduzione del video riprende, accertatevi che ogni chiamata `trackPause()` API sia associata a una chiamata `trackPlay()` API seguente.

* Scenari di tracciamento: Riproduzione [VOD senza annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso con l’SDK Chromecast per un esempio di tracciamento completo.

