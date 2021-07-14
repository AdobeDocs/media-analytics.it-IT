---
title: Scopri come tenere traccia della riproduzione core su Roku
description: Scopri come implementare il tracciamento di base utilizzando Media SDK su Roku.
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
exl-id: 5272c0ce-4e3d-48c6-bfa6-94066ccbf9ac
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 3%

---

# Tracciamento riproduzione core su Roku{#track-core-playback-on-roku}

>[!IMPORTANT]
>Questa documentazione tratta il tracciamento nella versione 2.x dell&#39;SDK. Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK](/help/sdk-implement/download-sdks.md)

1. **Configurazione del tracciamento iniziale**

   Identifica quando l&#39;utente attiva l&#39;intenzione di riproduzione (l&#39;utente fa clic su play e/o autoplay è attivato) e crea un&#39;istanza `MediaObject`.

   **`MediaObject`riferimento:**

   | Nome variable | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome video | Sì |
   | `mediaid` | Identificatore univoco del video | Sì |
   | `length` | Lunghezza del video | Sì |
   | `streamType` | Tipo di flusso (vedere _Costanti StreamType_ di seguito) | Sì |
   | `mediaType` | Tipo di supporto (vedi _Costanti MediaType_ di seguito) | Sì |

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

      [Implementazione dei metadati standard su Roku](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >Il collegamento dell&#39;oggetto metadati video standard all&#39;oggetto multimediale è facoltativo.

   * **Metadati personalizzati**

      Crea un oggetto variabile per le variabili personalizzate e inserisci i dati del video. Ad esempio:

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
   >`trackSessionStart` tiene traccia delle intenzioni dell&#39;utente in merito alla riproduzione, non dell&#39;inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati video e per stimare la metrica QoS time-to-start (la durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >Se non utilizzi metadati video personalizzati, invia semplicemente un oggetto vuoto per l’argomento `data` in `trackSessionStart`, come mostrato nella riga commento nell’esempio iOS precedente.

1. **Tracciare l&#39;inizio effettivo della riproduzione**

   Identifica l’evento dal lettore video per l’inizio della riproduzione del video, in cui viene eseguito il rendering del primo fotogramma del video sullo schermo, e chiama `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
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
   >`trackSessionEnd` segna la fine di una sessione di tracciamento video. Se la sessione è stata controllata correttamente al completamento, dove l’utente ha guardato il contenuto fino alla fine, assicurati che `trackComplete` venga chiamato prima di `trackSessionEnd`. Qualsiasi altra chiamata API `track*` viene ignorata dopo `trackSessionEnd`, tranne `trackSessionStart` per una nuova sessione di tracciamento video.

1. **Tracciare tutti gli scenari di pausa possibili**

   Identifica l&#39;evento dal lettore video per la pausa video e chiama `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Pausa scenari**

   Identifica qualsiasi scenario in cui il lettore video verrà messo in pausa e assicurati che `trackPause` sia chiamato correttamente. I seguenti scenari richiedono tutti che la chiamata all&#39;app `trackPause()`:

   * L’utente inserisce esplicitamente una pausa nell’app.
   * Il lettore si mette in stato di Pausa.
   * (*App mobili*) - L&#39;utente mette l&#39;applicazione in background, ma desideri che l&#39;app mantenga aperta la sessione.
   * (*App mobili*) - Si verifica un qualsiasi tipo di interruzione del sistema che causa lo sfondo di un&#39;applicazione. Ad esempio, l’utente riceve una chiamata, o si verifica un pop-up da un’altra applicazione, ma si desidera che l’applicazione mantenga in vita la sessione per dare all’utente la possibilità di riprendere il video dal punto di interruzione.

1. Identifica l&#39;evento dal lettore per la riproduzione video e/o la ripresa video dalla pausa e chiama `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >Può trattarsi della stessa origine evento utilizzata nel passaggio 4. Assicurati che ogni `trackPause()` chiamata API sia associata a una seguente chiamata `trackPlay()` API quando la riproduzione video riprende.

* Scenari di tracciamento: [Riproduzione VOD senza annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso con l’SDK Roku per un esempio di tracciamento completo.
