---
title: Scopri come tenere traccia della riproduzione core in Chromecast
description: Scopri come implementare il tracciamento core utilizzando Media SDK in Chromecast.
uuid: a9fc59d8-a2f4-4889-bdec-55c42a835d06
exl-id: 9812d06d-9efd-460c-a626-6a15f61a4c35
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/OOIzzdk-VT6rid11-Qzzg1qp2m1BWAsIx-aX4LXN4Gk
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 807
ht-degree: 85%

---

# Tracciare la riproduzione di base in Chromecast{#track-core-playback-on-chromecast}

Questa documentazione tratta il tracciamento nella versione 2.x dell’SDK.

>[!IMPORTANT]
>
>Se stai implementando una versione 1.x di SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK](/help/getting-started/download-sdks.md)

1. **Configurazione del tracciamento iniziale**

   Identifica quando l’utente attiva l’intenzione di riproduzione (l’utente fa clic su play e/o l’esecuzione automatica è attiva) e crea un’istanza `MediaObject`.

   Specifihe di **`MediaObject` API:**

   [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>);
   ```

   **`StreamType`Costanti:**

   [File multimediali ADBMobile](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`Costanti:**

   [File multimediali ADBMobile](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **Allegare metadati video**

   Facoltativamente, puoi allegare oggetti metadati video standard e/o personalizzati alla sessione di tracciamento video attraverso variabili dei dati di contesto.

   * **Metadati video standard**

     [Implementare i metadati standard in Chromecast](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

     >[!NOTE]
     >
     >Il collegamento dell’oggetto metadati video standard all’oggetto multimediale è facoltativo.

   * **Metadati personalizzati**

     Crea un oggetto variabile per le variabili personalizzate e lo popola con i dati del video. Ad esempio:

     ```js
     /* Set custom context data */
     var customVideoMetadata = {
         isUserLoggedIn: "false",
         tvStation: "Sample TV station",
         programmer: "Sample programmer"
     };
     ```

1. **Tracciare l’intenzione di inizio riproduzione**

   Per iniziare il tracciamento di una sessione multimediale, chiama [trackSessionStart](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart) sull’oggetto `media`.

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` tiene traccia delle intenzioni di riproduzione dell’utente, non dell’inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati video e per stimare la metrica QoS relativa al tempo di avvio (durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Il secondo valore corrisponde al nome dell’oggetto metadati video personalizzato creato nel passaggio 2. Se non utilizzi metadati video personalizzati, invia semplicemente un oggetto vuoto per l’argomento `data` in `trackSessionStart`, come mostrato nella riga esterna di commento nell’esempio di iOS precedente.

1. **Tracciare l’inizio effettivo della riproduzione**

   Identifica l’evento dal lettore video relativo all’inizio della riproduzione video, dove viene eseguito il rendering del primo fotogramma del video sullo schermo, e chiama [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay)

   ```
   ADBMobile.media.trackPlay();
   ```

1. **Aggiorna il valore della testina di riproduzione**

   Aggiorna il valore della posizione di `mediaUpdatePlayhead` più volte quando l&#39;indicatore di riproduzione cambia. <br /> Per il video on-demand (VOD), il valore è specificato in secondi dall’inizio dell’elemento multimediale. <br /> Per lo streaming live, se il lettore non fornisce informazioni sulla durata del contenuto, il valore può essere specificato come il numero di secondi trascorsi dalla mezzanotte UTC di quel giorno.

   ```
   ADBMobile().media.updatePlayhead(position)
   ```

   >[!NOTE]
   >
   >Quando si chiama l&#39;API `media.updatePlayhead`, tenere presente quanto segue:
   >* Quando si utilizzano i marcatori di avanzamento, è necessario specificare la durata del contenuto e la testina di riproduzione deve essere aggiornata come numero di secondi dall’inizio dell’elemento multimediale, a partire da 0.
   >* Quando si utilizzano Media SDK, è necessario chiamare l&#39;API `media.updatePlayhead` almeno una volta al secondo.

1. **Tracciare il completamento della riproduzione**

   Identifica l’evento dal lettore video relativo al completamento della riproduzione video, in cui l’utente ha guardato il contenuto fino alla fine, e chiama [trackComplete:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackComplete();
   ```

1. **Tracciare la fine della sessione**

   Identifica l’evento dal lettore video relativo allo scaricamento/chiusura della riproduzione video, in cui l’utente chiude il video e/o il video viene completato e scaricato, e chiama [trackSessionEnd:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd)

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` indica la fine di una sessione di tracciamento video. Se la sessione è stata vista correttamente fino al completamento, per cui l’utente ha guardato il contenuto fino alla fine, assicurati che `trackComplete` venga chiamato prima di `trackSessionEnd`. Dopo `trackSessionEnd`, qualsiasi chiamata API `track*` viene ignorata, tranne che la chiamata `trackSessionStart` per una nuova sessione di tracciamento video.

1. **Tracciare tutti gli scenari di pausa possibili**

   Identifica l’evento dal lettore video relativo alla sospensione video e chiama [trackPause:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause)

   ```
   ADBMobile.media.trackPause();
   ```

   **Scenari di pausa**

   Identifica uno scenario in cui il lettore video si interrompe e verifica che `trackPause` sia chiamato correttamente. Tutti gli scenari seguenti richiedono che l’app chiami `trackPause()`:

   * L’utente mette esplicitamente in pausa l’app.
   * Il lettore si mette in pausa da solo.
   * (*App per dispositivi mobili*): l’utente mette l’applicazione in background, ma si desidera invece che l’app mantenga aperta la sessione.
   * (*App mobili*): si verifica una qualsiasi interruzione del sistema causando l’esecuzione in background dell’applicazione. Ad esempio, l’utente riceve una chiamata oppure la notifica da un’altra applicazione, ma desideri che l’applicazione mantenga aperta la sessione per dare all’utente l’opportunità di riprendere il video dal punto in cui è stato interrotto.

1. Identifica l’evento dal lettore relativo alla riproduzione e/o la ripresa del video dalla sospensione e chiama [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >Potrebbe trattarsi della stessa origine evento utilizzata nel passaggio 4. Quando la riproduzione del video riprende, assicurati che ogni chiamata API `trackPause()` sia associata alla seguente chiamata API `trackPlay()`.

* Scenari di tracciamento: [riproduzione VOD senza annunci](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso nell’SDK di Chromecast per un esempio di tracciamento completo.
