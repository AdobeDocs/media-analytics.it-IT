---
title: Scopri come tenere traccia della riproduzione di base su Roku
description: Scopri come implementare il tracciamento della riproduzione di base utilizzando Media SDK su Roku.
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
exl-id: 5272c0ce-4e3d-48c6-bfa6-94066ccbf9ac
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 14329fab02e88cbad69ceea4ccd719b90f6555a6
workflow-type: ht
source-wordcount: '771'
ht-degree: 100%

---

# Tracciare la riproduzione di base in Roku {#track-core-playback-on-roku}

Questa documentazione tratta il tracciamento nella versione 2.x dell’SDK.

>[!IMPORTANT]
>Se stai implementando una versione 1.x di SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scarica SDK](/help/sdk-implement/download-sdks.md)

1. **Configurazione del tracciamento iniziale**

   Identifica quando l’utente attiva l’intenzione di riproduzione (l’utente fa clic su play e/o l’esecuzione automatica è attiva) e crea un’istanza `MediaObject`.

   Specifihe di **`MediaObject`:**

   | Nome variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome del video | Sì |
   | `mediaid` | Identificatore univoco del video | Sì |
   | `length` | Lunghezza video | Sì |
   | `streamType` | Tipo di flusso (vedi _Costanti StreamType_ sotto) | Sì |
   | `mediaType` | Tipo di file multimediale (vedi _Costanti MediaType_ sotto) | Sì |

   Costanti **`StreamType`:**

   | Nome costante | Descrizione   |
   |---|---|
   | `MEDIA_STREAM_TYPE_VOD` | Tipo di flusso per Video on Demand. |
   | `MEDIA_STREAM_TYPE_LIVE` | Tipo di flusso per il contenuto LIVE. |
   | `MEDIA_STREAM_TYPE_LINEAR` | Tipo di flusso per contenuti LINEAR. |
   | `MEDIA_STREAM_TYPE_AOD` | Tipo di flusso per audio on-demand |
   | `MEDIA_STREAM_TYPE_AUDIOBOOK` | Tipo di flusso per audiolibro |
   | `MEDIA_STREAM_TYPE_PODCAST` | Tipo di flusso per Podcast |

   Costanti **`MediaType`:**

   | Nome costante | Descrizione |
   |---|---|
   | `MEDIA_STREAM_TYPE_AUDIO` | Tipo di file multimediale per flussi Audio. |
   | `MEDIA_STREAM_TYPE_VIDEO` | Tipo di file multimediale per i flussi Video. |

   **Crea un oggetto informazioni multimediali per video con contenuto VOD:**

   ```
    mediaInfo = adb_media_init_mediainfo(
     "<MEDIA_NAME>",
     "<MEDIA_ID>",
     600,
     ADBMobile().MEDIA_STREAM_TYPE_VOD,
     ADBMobile().MEDIA_TYPE_VIDEO
   )
   ```

   oppure

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_VOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_VIDEO
   ```

   **Crea un oggetto informazioni multimediali per video con contenuto AOD:**

   ```
   mediaInfo = adb_media_init_mediainfo(
    "<MEDIA_NAME>",
    "<MEDIA_ID>",
    600,
    ADBMobile().MEDIA_STREAM_TYPE_AOD,
    ADBMobile().MEDIA_TYPE_AUDIO
   )
   ```

   oppure

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_AOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_AUDIO
   ```

1. **Allega metadati**

   Facoltativamente, allega oggetti metadati standard e/o personalizzati alla sessione di tracciamento tramite variabili di dati di contesto.

   * **Metadati standard**

[Implementare metadati standard in Roku](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >Il collegamento dell’oggetto metadati video standard all’oggetto multimediale è facoltativo.

   * **Metadati personalizzati**

      Crea un oggetto variabile per le variabili personalizzate e lo popola con i dati del video. Ad esempio:

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **Tracciare l’intenzione di inizio riproduzione**

   Per iniziare a tracciare una sessione multimediale, chiama `trackSessionStart` sull’istanza Media Heartbeat:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >Il secondo valore corrisponde al nome dell’oggetto metadati video personalizzato creato nel passaggio 2.

   >[!IMPORTANT]
   >`trackSessionStart` tiene traccia delle intenzioni dell’utente in merito alla riproduzione, non dell’inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati video e per stimare la metrica QoS relativa al tempo di avvio (durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >Se non utilizzi metadati video personalizzati, invia semplicemente un oggetto vuoto per l’argomento `data` in `trackSessionStart`, come mostrato nella riga esterna di commento nell’esempio di iOS precedente.

1. **Tracciare l’inizio effettivo della riproduzione**

   Identifica l’evento dal lettore video per l’inizio della riproduzione, in cui viene eseguito il rendering del primo fotogramma del video sullo schermo, quindi effettua una chiamata `trackPlay`.

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **Aggiorna il valore dell&#39;indicatore di riproduzione**

   Quando l&#39;indicatore di riproduzione multimediale viene modificato, notifica l’SDK effettuando una chiamata all’API `mediaUpdatePlayhead`. <br /> Per il tracciamento dei video on-demand (VOD), il valore è specificato in secondi dall’inizio dell’elemento multimediale. <br /> Per lo streaming live, se il lettore non fornisce informazioni sulla durata del contenuto, il valore può essere specificato come numero di secondi dalla mezzanotte UTC di quel giorno. <br /> Nota: quando si utilizzano i marcatori di avanzamento, è necessario specificare la durata del contenuto e la testina di riproduzione deve essere aggiornata come numero di secondi dall’inizio dell’elemento multimediale, a partire da 0.


   ```
   ADBMobile().mediaUpdatePlayhead(position)
   ```

1. **Tracciare il completamento della riproduzione**

   Identifica l’evento dal lettore video per il completamento della riproduzione, in cui l’utente ha guardato il contenuto fino alla fine, ed effettua una chiamata `trackComplete`.

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **Tracciamento della fine della sessione**

   Identifica l’evento dal lettore video per lo scaricamento/la chiusura della riproduzione, in cui l’utente chiude il video e/o il video viene completato e scaricato, quindi effettua una chiamata `trackSessionEnd`.

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` indica la fine di una sessione di tracciamento video. Se la sessione è stata vista correttamente fino al completamento, per cui l’utente ha guardato il contenuto fino alla fine, assicurati che `trackComplete` venga chiamato prima di `trackSessionEnd`. Dopo `trackSessionEnd`, qualsiasi chiamata API `track*` viene ignorata, tranne che la chiamata `trackSessionStart` per una nuova sessione di tracciamento video.

1. **Tracciare tutti gli scenari di pausa possibili**

   Identifica l’evento dal lettore video per la pausa video e la chiamata `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Scenari di pausa**

   Identifica uno scenario in cui il lettore video si interrompe e verifica che `trackPause` sia chiamato correttamente. I seguenti scenari richiedono tutti una chiamata `trackPause()` dall’app:

   * L’utente mette esplicitamente in pausa l’app.
   * Il lettore si mette in pausa da solo.
   * (*App per dispositivi mobili*): l’utente mette l’applicazione in background, ma si desidera invece che l’app mantenga aperta la sessione.
   * (*App per dispositivi mobili*): si verifica una qualsiasi interruzione del sistema causando l’esecuzione in background dell’applicazione. Ad esempio, l’utente riceve una chiamata oppure la notifica da un’altra applicazione, ma desideri che l’applicazione mantenga aperta la sessione per dare all’utente l’opportunità di riprendere il video dal punto in cui è stato interrotto.

1. Identifica l’evento dal lettore per la riproduzione video e/o la ripresa del video dalla pausa ed effettua una chiamata `trackPlay`.

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >Potrebbe trattarsi della stessa origine evento utilizzata nel passaggio 4. Quando la riproduzione del video riprende, assicurati che ogni chiamata API `trackPause()` sia associata alla seguente chiamata API `trackPlay()`.

* Scenari di tracciamento: [riproduzione VOD senza annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso con l’SDK Roku per un esempio di tracciamento completo.
