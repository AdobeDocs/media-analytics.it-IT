---
seo-title: Panoramica sul tracciamento
title: Panoramica sul tracciamento
uuid: 7 b 8 e 2 f 76-bc 4 e -4721-8933-3 e 4453 b 01788
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tracking Overview{#tracking-overview}

>[!IMPORTANT]
>
>Questa documentazione copre il tracciamento nella versione 2. x dell'SDK. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Eventi del lettore

Il tracciamento della riproduzione di base include il caricamento di supporti, l'avvio multimediale, la pausa media e il supporto per i file multimediali. Anche se non è obbligatorio, il buffering e la ricerca di tracciamento sono anche componenti core utilizzati per tenere traccia della riproduzione del contenuto. Nell'API per lettore multimediale, individua gli eventi del lettore che corrispondono alle chiamate di tracciamento di Media SDK, e codice i tuoi gestori di eventi per chiamare le API di tracciamento e per compilare le variabili obbligatorie e facoltative.

### Caricamento di contenuti multimediali

* Creare l'oggetto multimediale
* Compilazione dei metadati
* Call `trackSessionStart`; For example: `trackSessionStart(mediaObject, contextData)`

### Avvio multimediale

* Chiamata `trackPlay`

### Pausa/Ripresa

* Chiamata `trackPause`
* Call `trackPlay`   _when playback resumes_

### Contenuto multimediale completato

* Chiamata `trackComplete`

### Sull'interruzione del supporto

* Chiamata `trackSessionEnd`

### Avvio dello scorrimento

* Chiamata `trackEvent(SeekStart)`

### Lo scorrimento termina

* Chiamata `trackEvent(SeekComplete)`

### Avvio del buffering

* Chiamata `trackEvent(BufferStart);`

### Al termine del buffering

* Chiamata `trackEvent(BufferComplete);`

>[!TIP]
>
>La posizione della linea di scansione viene impostata come parte del codice di configurazione e di configurazione. For more information about `getCurrentPlayheadTime`, see [Overview: General Implementation Guidelines.](/help/sdk-implement/setup/setup-overview.md#section_965A3B699A8248DDB9B2B3EA3CC20E41)

## Implementate {#section_BB217BE6585D4EDEB34C198559575004}

1. **Configurazione di tracciamento iniziale -** Identificate quando l'utente attiva l'intento di riproduzione (l'utente fa clic su riproduzione e/o riproduzione automatica) e crea un `MediaObject` 'istanza utilizzando le informazioni sui supporti per il nome contenuto, l'ID contenuto, la lunghezza del contenuto e il tipo di streaming.

   **`MediaObject`riferimento:**

   | Nome della variabile | Descrizione | Obbligatorio |
   |---|---|---|
   | `name` | Nome contenuto | Sì |
   | `mediaid` | Identificatore univoco del contenuto | Sì |
   | `length` | Lunghezza contenuto | Sì |
   | `streamType` | Tipo di flusso | Sì |
   | `mediaType` | Tipo di file multimediale (contenuto audio o video) | Sì |

   **`StreamType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `VOD` | Tipo di flusso per Video su richiesta. |
   | `LIVE` | Tipo di flusso per il contenuto Live. |
   | `LINEAR` | Tipo di flusso per il contenuto lineare. |
   | `AOD` | Tipo di flusso per l'audio su richiesta |
   | `AUDIOBOOK` | Tipo di flusso per la rubrica audio |
   | `PODCAST` | Tipo di flusso per Podcast |

   **`MediaType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `Audio` | Tipo di file multimediale per i flussi audio. |
   | `Video` | Tipo di supporto per i flussi video. |

   The general format for creating the `MediaObject` is `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **Allega metadati -** Facoltativamente allega oggetti di metadati standard e/o personalizzati alla sessione di tracciamento attraverso variabili di dati contestuali.

   * **Metadati standard -**

      >[!NOTE]
      >
      >Allegare l'oggetto metadati standard all'oggetto multimediale è facoltativo.

      Crea un'istanza di un oggetto di metdati standard, compila le variabili desiderate e imposta l'oggetto metadati sull'oggetto Media Heartbeat.

      See the comprehensive list of metadata here: [Audio and video parameters.](/help/metrics-and-metadata/audio-video-parameters.md)

   * **Metadati personalizzati:** crea un oggetto variabile per le variabili personalizzate e popolate i dati per questo contenuto.

1. **Tracciate l'intenzione di avviare la riproduzione:** per iniziare a tracciare una sessione, chiamate `trackSessionStart` l'istanza Media Heartbeat.

   >[!IMPORTANT]
   >
   >`trackSessionStart` monitora l'intento utente di riproduzione, non l'inizio della riproduzione. This API is used to load the data/metadata and to estimate the time-to-start QoS metric (the time duration between `trackSessionStart` and `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom metadata, simply send an empty object for the `data` argument in `trackSessionStart`.

1. **Tracciate l'inizio effettivo della riproduzione:** identificate l'evento dal lettore multimediale all'inizio della riproduzione, dove viene eseguito il rendering del primo fotogramma del contenuto sullo schermo e chiamate `trackPlay`.

1. **Tenere traccia del completamento della riproduzione:** identificare l'evento dal lettore multimediale per completare la riproduzione, dove l'utente ha visualizzato il contenuto fino alla fine e richiamare `trackComplete`.

1. **Tracciare la fine della sessione -** Identificare l'evento dal lettore multimediale per lo scaricamento o la chiusura della riproduzione, dove l'utente chiude il contenuto e/o il contenuto è finito ed è stato scaricato e chiamato `trackSessionEnd`.

   >[!IMPORTANT]
   >
   >`trackSessionEnd` segna la fine di una sessione di tracciamento. If the session was successfully watched to completion, where the user watched the content until the end, ensure that `trackComplete` is called before `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.

1. **Tenere traccia di tutti i possibili scenari di pausa -** Identificare l'evento dal lettore multimediale per mettere in pausa e chiamare `trackPause`.

   **Scenari in pausa -** Identificate qualsiasi scenario in cui il lettore si interromperà e assicuratevi che `trackPause` venga chiamato correttamente. The following scenarios all require that your app call `trackPause()`:

   * L'utente si mette in pausa in modo esplicito nell'app.
   * Il lettore si attiva nello stato Pausa.
   * (*Mobile Apps*) - The user puts the application into the background, but you want the app to keep the session open.
   * (*Mobile Apps*) - Any type of system interrupt occurs that causes an application to be backgrounded. Ad esempio, l'utente riceve una chiamata oppure si verifica un pop-up da un'altra applicazione, ma si desidera che l'applicazione mantenga la sessione viva per consentire all'utente di riprendere il contenuto dal punto di interruzione.

1. Identify the event from the player for play and/or resume from pause and call `trackPlay`.

   >[!TIP]
   >
   >Potrebbe trattarsi della stessa origine dell'evento utilizzata al passaggio 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the playback resumes.

1. Ascoltare gli eventi di riproduzione della riproduzione dal lettore multimediale. On seek start event notification, track seeking using the `SeekStart` event.
1. On seek complete notification from the media player, track the end of seeking using the `SeekComplete` event.
1. Listen for the playback buffering events from media player, and on buffer start event notification, track buffering using the `BufferStart` event.
1. On buffer complete notification from the media player, track the end of buffering using the `BufferComplete` event.

Esempi di ogni passaggio nei seguenti argomenti specifici della piattaforma e guardate i lettori di esempio inclusi negli SDK.

Per un esempio semplice del tracciamento della riproduzione, consultate questo utilizzo dell'SDK javascript 2. x in un lettore HTML 5:

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
if (e.type == “buffering”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
}; 
 
/* Call on buffer complete */ 
if (e.type == “buffered”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
};
```

## Validate {#section_ABCFB92C587B4CAABDACF93452EFA78F}

### Inizio contenuto

All'inizio di un lettore multimediale, queste chiamate chiave vengono inviate nel seguente ordine:

1. Inizio analisi file multimediali
1. Avvio heartbeat
1. Analytics Analytics start

Le chiamate 1 e 2 contengono ulteriori variabili di metadati sia per le versioni personalizzate che per quelle standard.

### Riproduzione contenuto

Durante la riproduzione di contenuto principale normale, le chiamate Heartbeat vengono inviate al server Heartbeat ogni dieci secondi.

### Completamento contenuto

A 100% punti, sul contenuto o in corrispondenza di un bordo di visualizzazione su un flusso lineare, viene inviata una chiamata completa Heartbeat.

### Pausa contenuto

Quando il lettore viene messo in pausa, le chiamate all'evento pause del lettore verranno inviate ogni 10 secondi. Una volta terminata la pausa, gli eventi di riproduzione dovrebbero riprendere.

### Scorrimento contenuto B/Seek

Nello scorrimento dell'indicatore di riproduzione, non vengono inviate chiamate di tracciamento speciali. Tuttavia, quando la riproduzione riprende dopo lo scorrimento, il valore dell'indicatore di riproduzione deve riflettere la nuova posizione nel contenuto principale.

### Buffer contenuto

Quando i buffer del lettore multimediale sono buffer, le chiamate all'evento buffer del lettore vengono inviate ogni 10 secondi. Al termine del buffering, gli eventi di riproduzione dovrebbero riprendere.
