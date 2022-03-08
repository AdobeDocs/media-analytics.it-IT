---
title: Scopri come tenere traccia della riproduzione core in Chromecast
description: Scopri come implementare il tracciamento di base utilizzando Media SDK in Chromecast.
uuid: a9fc59d8-a2f4-4889-bdec-55c42a835d06
exl-id: 9812d06d-9efd-460c-a626-6a15f61a4c35
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 165c7f01a2d2c32df518c89a5c49637107d41086
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 0%

---

# Tracciamento riproduzione core in Chromecast{#track-core-playback-on-chromecast}

Questa documentazione tratta il tracciamento nella versione 2.x dell&#39;SDK.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK](/help/sdk-implement/download-sdks.md)

1. **Configurazione del tracciamento iniziale**

   Identifica quando l&#39;utente attiva l&#39;intenzione di riproduzione (l&#39;utente fa clic su play e/o l&#39;esecuzione automatica è attiva) e crea un `MediaObject` istanza.

   **`MediaObject`Riferimento API:**

   [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>);
   ```

   **`StreamType`costanti:**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`costanti:**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **Allegare metadati video**

   Facoltativamente, allega oggetti metadati video standard e/o personalizzati alla sessione di tracciamento video attraverso variabili di dati di contesto.

   * **Metadati video standard**

      [Implementazione dei metadati standard in Chromecast](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

      >[!NOTE]
      >
      >Il collegamento dell&#39;oggetto metadati video standard all&#39;oggetto multimediale è facoltativo.

   * **Metadati personalizzati**

      Crea un oggetto variabile per le variabili personalizzate e inserisci i dati del video. Esempio:

      ```js
      /* Set custom context data */
      var customVideoMetadata = {
          isUserLoggedIn: "false",
          tvStation: "Sample TV station",
          programmer: "Sample programmer"
      };
      ```

1. **Tracciare l&#39;intenzione di avviare la riproduzione**

   Per iniziare a monitorare una sessione multimediale, chiama [trackSessionStart](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart) sulla `media` oggetto.

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` tiene traccia delle intenzioni dell&#39;utente in merito alla riproduzione, non dell&#39;inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati video e per stimare la metrica di QoS time-to-start (la durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Il secondo valore è il nome dell&#39;oggetto metadati video personalizzato creato al passaggio 2. Se non utilizzi metadati video personalizzati, invia semplicemente un oggetto vuoto per `data` argomento in `trackSessionStart`, come mostrato nella riga commento nell’esempio di iOS precedente.

1. **Tracciare l&#39;inizio effettivo della riproduzione**

   Identifica l’evento dal lettore video per l’inizio della riproduzione del video, in cui viene eseguito il rendering del primo fotogramma del video sullo schermo, e chiama [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay)

   ```
   ADBMobile.media.trackPlay();
   ```

1. **Aggiorna il valore della testina di riproduzione**

   Aggiorna `mediaUpdatePlayhead`&#39; valore di posizione più volte quando il playhead cambia. <br /> Per il video-on-demand (VOD), il valore è specificato in secondi dall&#39;inizio dell&#39;elemento multimediale. <br /> Per lo streaming live, se il lettore non fornisce informazioni sulla durata del contenuto, il valore può essere specificato come numero di secondi dalla mezzanotte UTC di quel giorno. <br />  Nota: Quando si utilizzano i marcatori di avanzamento, è necessaria la durata del contenuto e l’indicatore di riproduzione deve essere aggiornato come numero di secondi dall’inizio dell’elemento multimediale, a partire da 0.

   ```
   ADBMobile().mediaUpdatePlayhead(position)
   ```

1. **Tracciare il completamento della riproduzione**

   Identifica l’evento dal lettore video per il completamento della riproduzione video, in cui l’utente ha guardato il contenuto fino alla fine, e chiama [trackComplete:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackComplete();
   ```

1. **Monitora la fine della sessione**

   Identifica l’evento dal lettore video per lo scaricamento/la chiusura della riproduzione video, in cui l’utente chiude il video e/o il video viene completato e scaricato, e chiama [trackSessionEnd:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd)

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` segna la fine di una sessione di tracciamento video. Se la sessione è stata controllata correttamente al completamento, dove l’utente ha guardato il contenuto fino alla fine, assicurati che `trackComplete` viene chiamato prima di `trackSessionEnd`. Qualsiasi altro `track*` La chiamata API viene ignorata dopo `trackSessionEnd`, tranne `trackSessionStart` per una nuova sessione di tracciamento video.

1. **Tracciare tutti gli scenari di pausa possibili**

   Identifica l’evento dal lettore video per la pausa video e la chiamata [trackPause:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause)

   ```
   ADBMobile.media.trackPause();
   ```

   **Pausa scenari**

   Identifica uno scenario in cui il lettore video si fermerà e assicurati che `trackPause` viene chiamato correttamente. I seguenti scenari richiedono tutti una chiamata all’app `trackPause()`:

   * L’utente inserisce esplicitamente una pausa nell’app.
   * Il lettore si mette in stato di Pausa.
   * (*App mobili*): l’utente mette l’applicazione in background, ma desideri che l’app mantenga aperta la sessione.
   * (*App mobili*) - Si verifica qualsiasi tipo di interruzione del sistema che causa lo sfondo di un&#39;applicazione. Ad esempio, l’utente riceve una chiamata, o si verifica un pop-up da un’altra applicazione, ma si desidera che l’applicazione mantenga in vita la sessione per dare all’utente la possibilità di riprendere il video dal punto di interruzione.

1. Identifica l&#39;evento dal lettore per la riproduzione video e/o la ripresa video dalla pausa e dalla chiamata [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >Può trattarsi della stessa origine evento utilizzata nel passaggio 4. Assicurati che ogni `trackPause()` La chiamata API è associata alla seguente `trackPlay()` Chiamata API quando la riproduzione del video riprende.

* Scenari di tracciamento: [Riproduzione VOD senza annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Sample player incluso con l’SDK di Chromecast per un esempio di tracciamento completo.
