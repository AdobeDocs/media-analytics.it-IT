---
title: Scopri come tenere traccia della riproduzione core su Roku
description: Scopri come implementare il tracciamento di base utilizzando Media SDK su Roku.
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
exl-id: 5272c0ce-4e3d-48c6-bfa6-94066ccbf9ac
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 14329fab02e88cbad69ceea4ccd719b90f6555a6
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 2%

---

# Tracciamento riproduzione core su Roku{#track-core-playback-on-roku}

Questa documentazione tratta il tracciamento nella versione 2.x dell&#39;SDK.

>[!IMPORTANT]
>Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK](/help/sdk-implement/download-sdks.md)

1. **Configurazione del tracciamento iniziale**

   Identifica quando l&#39;utente attiva l&#39;intenzione di riproduzione (l&#39;utente fa clic su play e/o l&#39;esecuzione automatica è attiva) e crea un `MediaObject` istanza.

   **`MediaObject`riferimento:**

   | Nome variable | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome video | Sì |
   | `mediaid` | Identificatore univoco del video | Sì |
   | `length` | Lunghezza del video | Sì |
   | `streamType` | Tipo di flusso (vedi _Costanti StreamType_ sotto) | Sì |
   | `mediaType` | Tipo di supporto (vedi _Costanti MediaType_ sotto) | Sì |

   **`StreamType`costanti:**

   | Nome costante | Descrizione   |
   |---|---|
   | `MEDIA_STREAM_TYPE_VOD` | Tipo di flusso per Video on Demand. |
   | `MEDIA_STREAM_TYPE_LIVE` | Tipo di flusso per il contenuto LIVE. |
   | `MEDIA_STREAM_TYPE_LINEAR` | Tipo di flusso per il contenuto LINEAR. |
   | `MEDIA_STREAM_TYPE_AOD` | Tipo di flusso per Audio On Demand |
   | `MEDIA_STREAM_TYPE_AUDIOBOOK` | Tipo di flusso per audio book |
   | `MEDIA_STREAM_TYPE_PODCAST` | Tipo di flusso per Podcast |

   **`MediaType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `MEDIA_STREAM_TYPE_AUDIO` | Tipo di supporto per flussi audio. |
   | `MEDIA_STREAM_TYPE_VIDEO` | Tipo di supporto per i flussi video. |

   **Crea un oggetto di informazioni multimediali per video con contenuto VOD:**

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

   **Crea un oggetto di informazioni multimediali per video con contenuto AOD:**

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
      >Il collegamento dell&#39;oggetto metadati video standard all&#39;oggetto multimediale è facoltativo.

   * **Metadati personalizzati**

      Crea un oggetto variabile per le variabili personalizzate e inserisci i dati del video. Esempio:

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **Tracciare l&#39;intenzione di avviare la riproduzione**

   Per iniziare a monitorare una sessione multimediale, chiama `trackSessionStart` sull&#39;istanza Media Heartbeat:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >Il secondo valore è il nome dell&#39;oggetto metadati video personalizzato creato al passaggio 2.

   >[!IMPORTANT]
   >`trackSessionStart` tiene traccia delle intenzioni dell&#39;utente in merito alla riproduzione, non dell&#39;inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati video e per stimare la metrica di QoS time-to-start (la durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >Se non utilizzi metadati video personalizzati, invia semplicemente un oggetto vuoto per `data` argomento in `trackSessionStart`, come mostrato nella riga commento nell’esempio di iOS precedente.

1. **Tracciare l&#39;inizio effettivo della riproduzione**

   Identifica l’evento dal lettore video per l’inizio della riproduzione del video, in cui viene eseguito il rendering del primo fotogramma del video sullo schermo, e chiama `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **Aggiorna il valore della testina di riproduzione**

   Quando la testina di riproduzione multimediale cambia, notifica l&#39;SDK chiamando `mediaUpdatePlayhead` API. <br /> Per il video-on-demand (VOD), il valore è specificato in secondi dall&#39;inizio dell&#39;elemento multimediale. <br /> Per lo streaming live, se il lettore non fornisce informazioni sulla durata del contenuto, il valore può essere specificato come numero di secondi dalla mezzanotte UTC di quel giorno. <br /> Nota: Quando si utilizzano i marcatori di avanzamento, è necessaria la durata del contenuto e l’indicatore di riproduzione deve essere aggiornato come numero di secondi dall’inizio dell’elemento multimediale, a partire da 0.


   ```
   ADBMobile().mediaUpdatePlayhead(position)
   ```

1. **Tracciare il completamento della riproduzione**

   Identifica l’evento dal lettore video per il completamento della riproduzione video, in cui l’utente ha guardato il contenuto fino alla fine, e chiama `trackComplete`:

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **Monitora la fine della sessione**

   Identifica l’evento dal lettore video per lo scaricamento/la chiusura della riproduzione video, in cui l’utente chiude il video e/o il video viene completato e scaricato, e chiama `trackSessionEnd`:

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` segna la fine di una sessione di tracciamento video. Se la sessione è stata controllata correttamente al completamento, dove l’utente ha guardato il contenuto fino alla fine, assicurati che `trackComplete` viene chiamato prima di `trackSessionEnd`. Qualsiasi altro `track*` La chiamata API viene ignorata dopo `trackSessionEnd`, tranne `trackSessionStart` per una nuova sessione di tracciamento video.

1. **Tracciare tutti gli scenari di pausa possibili**

   Identifica l’evento dal lettore video per la pausa video e la chiamata `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Pausa scenari**

   Identifica uno scenario in cui il lettore video si fermerà e assicurati che `trackPause` viene chiamato correttamente. I seguenti scenari richiedono tutti una chiamata all’app `trackPause()`:

   * L’utente inserisce esplicitamente una pausa nell’app.
   * Il lettore si mette in stato di Pausa.
   * (*App mobili*): l’utente mette l’applicazione in background, ma desideri che l’app mantenga aperta la sessione.
   * (*App mobili*) - Si verifica qualsiasi tipo di interruzione del sistema che causa lo sfondo di un&#39;applicazione. Ad esempio, l’utente riceve una chiamata, o si verifica un pop-up da un’altra applicazione, ma si desidera che l’applicazione mantenga in vita la sessione per dare all’utente la possibilità di riprendere il video dal punto di interruzione.

1. Identifica l&#39;evento dal lettore per la riproduzione video e/o la ripresa video dalla pausa e dalla chiamata `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >Può trattarsi della stessa origine evento utilizzata nel passaggio 4. Assicurati che ogni `trackPause()` La chiamata API è associata alla seguente `trackPlay()` Chiamata API quando la riproduzione del video riprende.

* Scenari di tracciamento: [Riproduzione VOD senza annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso con l’SDK Roku per un esempio di tracciamento completo.
