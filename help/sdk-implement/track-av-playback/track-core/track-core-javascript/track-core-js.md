---
title: Scopri Come Tracciare La Riproduzione Core Utilizzando JavaScript 2.x
description: Scopri come implementare il tracciamento di base utilizzando Media SDK in un browser utilizzando le app JavaScript 2.x.
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab
exl-id: d8af37a0-9048-4e6b-8cba-809386cbed5f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 3%

---

# Tracciamento riproduzione core con JavaScript 2.x{#track-core-playback-on-javascript}

>[!IMPORTANT]
>Questa documentazione tratta il tracciamento nella versione 2.x dell&#39;SDK. Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK](/help/sdk-implement/download-sdks.md)

1. **Configurazione del tracciamento iniziale**

   Identifica quando l&#39;utente attiva l&#39;intenzione di riproduzione (l&#39;utente fa clic su play e/o autoplay è attivato) e crea un&#39;istanza `MediaObject`.

   [API createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nome variable | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome file multimediale | Sì |
   | `mediaid` | Identificatore univoco del supporto | Sì |
   | `length` | Lunghezza del supporto | Sì |
   | `streamType` | Tipo di flusso (vedere _Costanti StreamType_ di seguito) | Sì |
   | `mediaType` | Tipo di supporto (vedi _Costanti MediaType_ di seguito) | Sì |

   **`StreamType`costanti:**

   | Nome costante | Descrizione   |
   |---|---|
   | `VOD` | Tipo di flusso per Video on Demand. |
   | `LIVE` | Tipo di flusso per il contenuto LIVE. |
   | `LINEAR` | Tipo di flusso per il contenuto LINEAR. |
   | `AOD` | Tipo di flusso per Audio on Demand. |
   | `AUDIOBOOK` | Tipo di flusso per Audio Book. |
   | `PODCAST` | Tipo di flusso per Podcast. |

   **`MediaType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `Audio` | Tipo di supporto per flussi audio. |
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

   Facoltativamente, allega oggetti metadati standard e/o personalizzati alla sessione di tracciamento tramite variabili di dati di contesto.

   * **Metadati standard**

      [Implementazione dei metadati standard in JavaScript](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >Il collegamento dell&#39;oggetto metadati standard all&#39;oggetto multimediale è facoltativo.

      * Riferimento API per le chiavi dei metadati multimediali - [chiavi dei metadati standard - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         Vedi il set completo dei metadati disponibili qui: [Parametri audio e video](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Metadati personalizzati**

      Crea un oggetto variabile per le variabili personalizzate e compila i dati per questo supporto. Ad esempio:

      ```js
      /* Set custom context data */
      var customVideoMetadata = {
          isUserLoggedIn: "false",
          tvStation: "Sample TV station",
          programmer: "Sample programmer"
      };
      ```


1. **Tracciare l&#39;intenzione di avviare la riproduzione**

   Per iniziare a monitorare una sessione multimediale, chiama `trackSessionStart` sull&#39;istanza Media Heartbeat:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >Il secondo valore è il nome dell&#39;oggetto metadati multimediali personalizzati creato al passaggio 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` tiene traccia delle intenzioni dell&#39;utente in merito alla riproduzione, non dell&#39;inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati e per stimare la metrica QoS time-to-start (la durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzi metadati personalizzati, invia semplicemente un oggetto vuoto per l’argomento `data` in `trackSessionStart`, come mostrato nella riga commento nell’esempio iOS precedente.

1. **Tracciare l&#39;inizio effettivo della riproduzione**

   Identificare l&#39;evento dal lettore multimediale per l&#39;inizio della riproduzione, dove viene eseguito il rendering del primo fotogramma del file multimediale sullo schermo, e chiamare `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Tracciare il completamento della riproduzione**

   Identificare l&#39;evento dal lettore multimediale per il completamento della riproduzione, dove l&#39;utente ha guardato il contenuto fino alla fine, e chiamare `trackComplete`:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Monitora la fine della sessione**

   Identificare l&#39;evento dal lettore multimediale per lo scaricamento/la chiusura della riproduzione, in cui l&#39;utente chiude il supporto e/o il supporto è stato completato e scaricato, e chiamare `trackSessionEnd`:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` segna la fine di una sessione di tracciamento. Se la sessione è stata controllata correttamente al completamento, dove l’utente ha guardato il contenuto fino alla fine, assicurati che `trackComplete` venga chiamato prima di `trackSessionEnd`. Qualsiasi altra chiamata API `track*` viene ignorata dopo `trackSessionEnd`, tranne `trackSessionStart` per una nuova sessione di tracciamento.

1. **Tracciare tutti gli scenari di pausa possibili**

   Identifica l&#39;evento dal lettore multimediale per la pausa e la chiamata `trackPause`:

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Pausa scenari**

   Identifica qualsiasi scenario in cui il lettore multimediale si mette in pausa e assicurati che `trackPause` sia chiamato correttamente. I seguenti scenari richiedono tutti che la chiamata all&#39;app `trackPause()`:

   * L’utente inserisce esplicitamente una pausa nell’app.
   * Il lettore si mette in stato di Pausa.
   * (*App mobili*) - L&#39;utente mette l&#39;applicazione in background, ma desideri che l&#39;app mantenga aperta la sessione.
   * (*App mobili*) - Si verifica un qualsiasi tipo di interruzione del sistema che causa lo sfondo di un&#39;applicazione. Ad esempio, l&#39;utente riceve una chiamata, o si verifica un pop-up da un&#39;altra applicazione, ma si desidera che l&#39;applicazione mantenga in vita la sessione per dare all&#39;utente la possibilità di riprendere il supporto dal punto di interruzione.

1. Identifica l&#39;evento dal lettore per la riproduzione e/o la ripresa dalla pausa e chiama `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >Può trattarsi della stessa origine evento utilizzata nel passaggio 4. Assicurati che ogni chiamata API `trackPause()` sia associata a una seguente chiamata API `trackPlay()` quando la riproduzione riprende.

* Scenari di tracciamento: [Riproduzione VOD senza annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Lettore di esempio incluso nell&#39;SDK JavaScript per un esempio di tracciamento completo.
