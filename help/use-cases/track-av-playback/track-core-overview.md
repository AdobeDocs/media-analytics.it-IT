---
title: Informazioni sul tracciamento della riproduzione dei contenuti
description: "Scopri come tracciare la riproduzione core, compresi il caricamento, l’avvio, la messa in pausa e il completamento del contenuto multimediale. "
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 98%

---

# Panoramica del tracciamento {#tracking-overview}

Questa documentazione tratta il tracciamento nella versione 2.x dell’SDK.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/getting-started/download-sdks.md)

## Eventi del lettore

Il tracciamento della riproduzione core include il tracciamento degli eventi di caricamento, avvio, pausa e completamento dei contenuti multimediali. Sebbene non siano obbligatori, anche il tracciamento di buffering e ricerca sono componenti core utilizzati per il tracciamento della riproduzione dei contenuti. Nell’API del lettore multimediale, identifica gli eventi corrispondenti alle chiamate di tracciamento Media SDK e codifica i gestori di eventi per chiamare le API di tracciamento e per popolare le variabili obbligatorie e facoltative.

### Al caricamento del contenuto multimediale

* Crea l’oggetto multimediale
* Popola i metadati
* Effettua la chiamata `trackSessionStart`; ad esempio: `trackSessionStart(mediaObject, contextData)`

### All’avvio del contenuto multimediale

* Effettua la chiamata `trackPlay`

### Alla pausa/ripresa

* Effettua la chiamata `trackPause`
* Effettua la chiamata `trackPlay`  _quando riprende la riproduzione_

### Al completamento del contenuto multimediale

* Effettua la chiamata `trackComplete`

### All’interruzione del contenuto multimediale

* Effettua la chiamata `trackSessionEnd`

### Quando inizia lo scorrimento

* Effettua la chiamata `trackEvent(SeekStart)`

### Quando termina lo scorrimento

* Effettua la chiamata `trackEvent(SeekComplete)`
Annulla modifiche

### Quando inizia il buffering

* Effettua la chiamata `trackEvent(BufferStart);`

### Quando termina il buffering

* Effettua la chiamata `trackEvent(BufferComplete);`

>[!TIP]
>
>La posizione della testina di riproduzione viene impostata nel codice di impostazione e configurazione. Per ulteriori informazioni su `getCurrentPlayheadTime`, consulta [Panoramica: linee guida generali per l’implementazione](/help/implementation/media-sdk/media-sdk-overview.md)


## Implementazione {#implement}

1. **Configurazione iniziale del tracciamento -** Identifica quando l’utente attiva l’intenzione di riproduzione (l’utente fa clic su play e/o è attiva la riproduzione automatica) e crea un’istanza di `MediaObject` che utilizza le informazioni del contenuto multimediale relative a nome, ID e durata e tipo di flusso.

   Specifihe di **`MediaObject`:**

   | Nome variabile | Descrizione | Obbligatorio |
   |---|---|---|
   | `name` | Nome del contenuto | Sì |
   | `mediaid` | Identificatore univoco del contenuto | Sì |
   | `length` | Durata del contenuto | Sì |
   | `streamType` | Tipo di flusso | Sì |
   | `mediaType` | Tipo contenuto (audio o video) | Sì |

   Costanti **`StreamType`:**

   | Nome costante | Descrizione |
   |---|---|
   | `VOD` | Tipo di flusso per Video on Demand. |
   | `LIVE` | Tipo di flusso per il contenuto Live. |
   | `LINEAR` | Tipo di flusso per contenuti Linear. |
   | `AOD` | Tipo di flusso per audio on-demand |
   | `AUDIOBOOK` | Tipo di flusso per audiolibro |
   | `PODCAST` | Tipo di flusso per Podcast |

   Costanti **`MediaType`:**

   | Nome costante | Descrizione |
   |---|---|
   | `Audio` | Tipo di file multimediale per flussi Audio. |
   | `Video` | Tipo di file multimediale per i flussi Video. |

   Il formato generale per la creazione di `MediaObject` è `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **Allega metadati -** Facoltativamente allega oggetti metadati standard e/o personalizzati alla sessione di tracciamento tramite variabili di dati contestuali.

   * **Metadati standard -**

      >[!NOTE]
      >
      >Il collegamento dell’oggetto metadati standard all’oggetto multimediale è facoltativo.

      Crea un’istanza di un oggetto metadata standard, popola le variabili desiderate e imposta l’oggetto metadati sull’oggetto Media Heartbeat.

      Per un elenco completo dei metadati, consulta [Parametri audio e video.](../../implementation/variables/audio-video-parameters.md)

   * **Metadati personalizzati -** Crea un oggetto variabile per le variabili personalizzate e lo popola con i dati per questo contenuto.

1. **Tracciare l’intenzione di inizio riproduzione -** Per iniziare a tracciare una sessione, effettua la chiamata `trackSessionStart` sull’istanza Media Heartbeat.

   >[!IMPORTANT]
   >
   >`trackSessionStart` traccia l’intenzione dell’utente di iniziare la riproduzione, ma non l’inizio della riproduzione stessa. Questa API viene utilizzata per caricare dati/metadati e per stimare la metrica di qualità del servizio relativa al tempo necessario per l’avvio (tempo che trascorre ta `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzi metadati personalizzati, è sufficiente inviare un oggetto vuoto per l’argomento `data` in `trackSessionStart`.

1. **Tracciare l’inizio effettivo della riproduzione -** Identifica l’evento dal lettore multimediale relativo all’inizio della riproduzione, ossia al rendering del primo fotogramma del contenuto sullo schermo, ed effettua la chiamata `trackPlay`.

1. **Tracciare il completamento della riproduzione -** Identifica l’evento dal lettore multimediale relativo al completamento della riproduzione, ossia al momento in cui l’utente ha guardato il contenuto fino alla fine, ed effettua la chiamata `trackComplete`.

1. **Tracciare la fine della sessione -** Identifica l’evento dal lettore multimediale relativo a scaricamento/chiusura della riproduzione, ossia qundo cui l’utente chiude il contenuto e/o il contenuto è stato completato e quindi non è più caricato, ed effettua la chiamata `trackSessionEnd`.

   >[!IMPORTANT]
   >
   >`trackSessionEnd` indica la fine di una sessione di tracciamento. Se la sessione è stata guardata correttamente fino al completamento, dove l’utente ha guardato il contenuto fino alla fine, assicurati che `trackComplete` venga chiamato prima di `trackSessionEnd`. Qualsiasi altra chiamata API `track*` viene ignorata dopo `trackSessionEnd`, tranne `trackSessionStart` per una nuova sessione di tracciamento.

1. **Tracciare tutti i possibili scenari di pausa -** Identifica l’evento dal lettore multimediale relativo alla sospensione e chiama `trackPause`.

   **Scenari di pausa -** Identifica qualsiasi scenario in cui il lettore effettua una pausa e si assicura che `trackPause` venga chiamato correttamente. Tutti gli scenari seguenti richiedono che l’app chiami `trackPause()`:

   * L’utente mette esplicitamente in pausa l’app.
   * Il lettore si mette in pausa da solo.
   * (*App per dispositivi mobili*): l’utente mette l’applicazione in background, ma si desidera invece che l’app mantenga aperta la sessione.
   * (*App mobili*): si verifica una qualsiasi interruzione del sistema causando l’esecuzione in background dell’applicazione. Ad esempio, l’utente riceve una chiamata o viene visualizzato un pop-up da un’altra applicazione, ma si desidera che l’applicazione mantenga attiva la sessione dando all’utente la possibilità di riprendere il contenuto dal punto di interruzione.

1. Identifica l&#39;evento dal lettore relativo alla riproduzione e/o la ripresa dalla sospensione e chiama `trackPlay`.

   >[!TIP]
   >
   >Potrebbe trattarsi della stessa origine evento utilizzata nel passaggio 4. Assicurati che ogni chiamata API `trackPause()` sia associata a una seguente `trackPlay()` quando riprende la riproduzione.

1. Ascolta gli eventi di ricerca della riproduzione dal lettore multimediale. Alla notifica dell’evento di inizio ricerca, traccia la ricerca utilizzando l’evento `SeekStart`.
1. Alla notifica del completamento della ricerca dal lettore multimediale, traccia la fine della ricerca utilizzando l’evento `SeekComplete`.
1. Ascolta gli eventi di buffering della riproduzione dal lettore multimediale e alla notifica dell’evento di inizio buffer, traccia il buffering utilizzando l’evento `BufferStart`.
1. Alla notifica del completamento del buffering dal lettore multimediale, traccia la fine del buffering utilizzando l’evento `BufferComplete`.

Consulta gli esempi relativi a ciascun passaggio nei seguenti argomenti specifici per piattaforma e vedi i lettori di esempio inclusi negli SDK.

Per avere un semplice esempio di tracciamento della riproduzione, consulta questo utilizzo dell’SDK JavaScript 2.x in un lettore HTML5:

```js
/* Call on media start */
if (e.type == "play") {

    // Check for start of media
    if (!sessionStarted) {
        /* Set media info */     
        /* MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                            <MEDIA_ID>,  
                                            <MEDIA_LENGTH>,
                                            <MEDIA_STREAMTYPE>,
                                            <MEDIA_MEDIATYPE>);*/
        var mediaInfo = MediaHeartbeat.createMediaObject(
          document.getElementsByTagName('video')[0].getAttribute("name"),  
          document.getElementsByTagName('video')[0].getAttribute("id"),  
          video.duration,
          MediaHeartbeat.StreamType.VOD);

        /* Set custom context data */
        var customVideoMetadata = {
            isUserLoggedIn: "false",
            tvStation: "Sample TV station",
            programmer: "Sample programmer"
        };

        /* Set standard video metadata */     
        var standardVideoMetadata = {};
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode";
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show";
        mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,  
                           standardVideoMetadata);     

        // Start Session
        this.mediaHeartbeat.trackSessionStart(mediaInfo, customVideoMetadata);    

        // Track play
        this.mediaHeartbeat.trackPlay();  
        sessionStarted = true;     

    } else {
        // Track play for resuming playack    
        this.mediaHeartbeat.trackPlay();  
    }
};

/* Call on video complete */
if (e.type == "ended") {
    console.log("video ended");
    this.mediaHeartbeat.trackComplete();
    this.mediaHeartbeat.trackSessionEnd();
    sessionStarted = false;     
};

/* Call on pause */
if (e.type == "pause") {
    this.mediaHeartbeat.trackPause();
};

/* Call on scrub start */
if (e.type == "seeking") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
};

/* Call on scrub stop */
if (e.type == "seeked") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
};

/* Call on buffer start */
if (e.type == "buffering") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
};

/* Call on buffer complete */
if (e.type == "buffered") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

## Convalida {#validate}

Per informazioni sulla convalida della *legacy* implementazione, vedi [Convalida legacy.](/help/legacy/validation/validation-overview.md)
