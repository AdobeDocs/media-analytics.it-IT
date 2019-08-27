---
seo-title: Panoramica sul tracciamento
title: Panoramica sul tracciamento
uuid: 7 b 8 e 2 f 76-bc 4 e -4721-8933-3 e 4453 b 01788
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Panoramica sul tracciamento{#tracking-overview}

>[!IMPORTANT]
>
>Questa documentazione copre il tracciamento nella versione 2. x dell'SDK. Se implementhi una versione 1. x dell'SDK, puoi scaricare le guide per sviluppatori 1. x qui: [Scarica gli SDK.](/help/sdk-implement/download-sdks.md)

## Eventi del lettore

Il tracciamento della riproduzione di base include il caricamento di supporti, l'avvio multimediale, la pausa media e il supporto per i file multimediali. Anche se non è obbligatorio, il buffering e la ricerca di tracciamento sono anche componenti core utilizzati per tenere traccia della riproduzione del contenuto. Nell'API per lettore multimediale, individua gli eventi del lettore che corrispondono alle chiamate di tracciamento di Media SDK, e codice i tuoi gestori di eventi per chiamare le API di tracciamento e per compilare le variabili obbligatorie e facoltative.

### Caricamento di contenuti multimediali

* Creare l'oggetto multimediale
* Compilazione dei metadati
* Chiamata `trackSessionStart`; Ad esempio: `trackSessionStart(mediaObject, contextData)`

### Avvio multimediale

* Chiamata `trackPlay`

### Pausa/Ripresa

* Chiamata `trackPause`
* Chiamata  `trackPlay`_alla ripresa della riproduzione_

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
>La posizione della linea di scansione viene impostata come parte del codice di configurazione e di configurazione. Per ulteriori informazioni, `getCurrentPlayheadTime`consulta [Panoramica: Linee guida generali sull'implementazione.](/help/sdk-implement/setup/setup-overview.md#section_965A3B699A8248DDB9B2B3EA3CC20E41)

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

   Il formato generale per la creazione `MediaObject` di `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **Allega metadati -** Facoltativamente allega oggetti di metadati standard e/o personalizzati alla sessione di tracciamento attraverso variabili di dati contestuali.

   * **Metadati standard -**

      >[!NOTE]
      >
      >Allegare l'oggetto metadati standard all'oggetto multimediale è facoltativo.

      Crea un'istanza di un oggetto di metdati standard, compila le variabili desiderate e imposta l'oggetto metadati sull'oggetto Media Heartbeat.

      Consultate l'elenco completo dei metadati qui: [Parametri audio e video.](/help/metrics-and-metadata/audio-video-parameters.md)

   * **Metadati personalizzati:** crea un oggetto variabile per le variabili personalizzate e popolate i dati per questo contenuto.

1. **Tracciate l'intenzione di avviare la riproduzione:** per iniziare a tracciare una sessione, chiamate `trackSessionStart` l'istanza Media Heartbeat.

   >[!IMPORTANT]
   >
   >`trackSessionStart` monitora l'intento utente di riproduzione, non l'inizio della riproduzione. Questa API viene utilizzata per caricare dati/metadati e per stimare la metrica Time-to-start qos (durata temporale tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzate metadati personalizzati, inviate semplicemente un oggetto vuoto per l' `data` argomento in `trackSessionStart`.

1. **Tracciate l'inizio effettivo della riproduzione:** identificate l'evento dal lettore multimediale all'inizio della riproduzione, dove viene eseguito il rendering del primo fotogramma del contenuto sullo schermo e chiamate `trackPlay`.

1. **Tenere traccia del completamento della riproduzione:** identificare l'evento dal lettore multimediale per completare la riproduzione, dove l'utente ha visualizzato il contenuto fino alla fine e richiamare `trackComplete`.

1. **Tracciare la fine della sessione -** Identificare l'evento dal lettore multimediale per lo scaricamento o la chiusura della riproduzione, dove l'utente chiude il contenuto e/o il contenuto è finito ed è stato scaricato e chiamato `trackSessionEnd`.

   >[!IMPORTANT]
   >
   >`trackSessionEnd` segna la fine di una sessione di tracciamento. Se la sessione è stata visualizzata in modo corretto, in cui l'utente ha visualizzato il contenuto fino alla fine, assicuratevi che `trackComplete` venga richiamata prima `trackSessionEnd`. Qualsiasi altra `track*` chiamata API viene ignorata dopo `trackSessionEnd`, fatta eccezione per `trackSessionStart` una nuova sessione di tracciamento.

1. **Tenere traccia di tutti i possibili scenari di pausa -** Identificare l'evento dal lettore multimediale per mettere in pausa e chiamare `trackPause`.

   **Scenari in pausa -** Identificate qualsiasi scenario in cui il lettore si interromperà e assicuratevi che `trackPause` venga chiamato correttamente. Gli scenari seguenti richiedono che la chiamata all'app sia chiamata `trackPause()`:

   * L'utente si mette in pausa in modo esplicito nell'app.
   * Il lettore si attiva nello stato Pausa.
   * (*App mobili*): l'utente inserisce l'applicazione in background, ma desiderate che l'app rimanga aperta.
   * (*App mobili*): si verifica un qualsiasi tipo di interruzione di sistema che causa la messa in background di un'applicazione. Ad esempio, l'utente riceve una chiamata oppure si verifica un pop-up da un'altra applicazione, ma si desidera che l'applicazione mantenga la sessione viva per consentire all'utente di riprendere il contenuto dal punto di interruzione.

1. Identificare l'evento dal lettore per la riproduzione e/o riprendere dalla pausa e chiamare `trackPlay`.

   >[!TIP]
   >
   >Potrebbe trattarsi della stessa origine dell'evento utilizzata al passaggio 4. Assicuratevi che ogni `trackPause()` chiamata API sia associata a una chiamata API successiva `trackPlay()` al momento della ripresa della riproduzione.

1. Ascoltare gli eventi di riproduzione della riproduzione dal lettore multimediale. Nella notifica di avvio dell'evento, tracciare la ricerca utilizzando l' `SeekStart` evento.
1. In ricerca di una notifica completa dal lettore multimediale, tracciate la fine della ricerca utilizzando l' `SeekComplete` evento.
1. Ascoltare gli eventi di buffering di riproduzione dal lettore multimediale e sulla notifica dell'evento iniziale del buffer, tracciare il buffering utilizzando l `BufferStart` 'evento.
1. Al buffer completo di una notifica dal lettore multimediale, tracciate la fine del buffering utilizzando l' `BufferComplete` evento.

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

## Convalida {#section_ABCFB92C587B4CAABDACF93452EFA78F}

Per informazioni sulla convalida della propria implementazione, vedere [Convalida.](/help/sdk-implement/validation/validation-overview.md)

