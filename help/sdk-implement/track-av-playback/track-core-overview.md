---
seo-title: Panoramica di tracciamento
title: Panoramica di tracciamento
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# Panoramica di tracciamento{#tracking-overview}

>[!IMPORTANT]
>
>Questa documentazione descrive il tracciamento nella versione 2.x dell’SDK. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Eventi del lettore

Il tracciamento della riproduzione di base include il caricamento del supporto, l'avvio del supporto, la pausa del supporto e il completamento del supporto. Sebbene non sia obbligatorio, il buffering di tracciamento e la ricerca sono anche componenti di base utilizzati per tenere traccia della riproduzione dei contenuti. Nell’API del lettore multimediale, identificate gli eventi del lettore che corrispondono alle chiamate di tracciamento di Media SDK e codificate i gestori di eventi per chiamare le API di tracciamento e per compilare le variabili obbligatorie e facoltative.

### Al caricamento del supporto

* Creare l'oggetto multimediale
* Compilare i metadati
* Invito `trackSessionStart`;Ad esempio: `trackSessionStart(mediaObject, contextData)`

### All'avvio del supporto

* Chiamata `trackPlay`

### In pausa/ripresa

* Chiamata `trackPause`
* Chiamata `trackPlay` _quando la riproduzione riprende_

### Supporto completo

* Chiamata `trackComplete`

### In caso di interruzione del supporto

* Chiamata `trackSessionEnd`

### Quando inizia lo scorrimento

* Chiamata `trackEvent(SeekStart)`

### Quando lo scorrimento termina

* Chiamata `trackEvent(SeekComplete)`

### Quando inizia il buffering

* Chiamata `trackEvent(BufferStart);`

### Quando il buffering termina

* Chiamata `trackEvent(BufferComplete);`

>[!TIP]
>
>La posizione dell'indicatore di riproduzione è impostata nel codice di configurazione e configurazione. Per ulteriori informazioni su `getCurrentPlayheadTime`, consulta [Panoramica: Linee guida generali sull’implementazione](/help/sdk-implement/setup/setup-overview.md#general-implementation-guidelines)

## Implementate {#implement}

1. **Configurazione iniziale tracciamento: identificate quando l'utente attiva l'intenzione di riproduzione (l'utente fa clic su play e/o la riproduzione automatica è attivata) e create un'** `MediaObject` istanza utilizzando le informazioni sui supporti per il nome del contenuto, l'ID del contenuto, la lunghezza del contenuto e il tipo di flusso.

   **`MediaObject`riferimento:**

   | Nome della variabile | Descrizione | Obbligatorio |
   |---|---|---|
   | `name` | Nome contenuto | Sì |
   | `mediaid` | Identificatore univoco contenuto | Sì |
   | `length` | Lunghezza contenuto | Sì |
   | `streamType` | Tipo di flusso | Sì |
   | `mediaType` | Tipo di supporto (contenuto audio o video) | Sì |

   **`StreamType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `VOD` | Tipo di flusso per Video on Demand. |
   | `LIVE` | Tipo di flusso per il contenuto live. |
   | `LINEAR` | Tipo di flusso per il contenuto lineare. |
   | `AOD` | Tipo di flusso per l'audio su richiesta |
   | `AUDIOBOOK` | Tipo di flusso per la rubrica audio |
   | `PODCAST` | Tipo di flusso per Podcast |

   **`MediaType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `Audio` | Tipo di supporto per i flussi audio. |
   | `Video` | Tipo di supporto per i flussi video. |

   Il formato generale per la creazione di `MediaObject``MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **Allega metadati - (Facoltativo): allega** oggetti metadati standard e/o personalizzati alla sessione di tracciamento tramite variabili di dati contestuali.

   * **Metadati standard -**

      >[!NOTE]
      >
      >Il collegamento dell'oggetto metadati standard all'oggetto multimediale è facoltativo.

      Creare un'istanza di un oggetto metdata standard, compilare le variabili desiderate e impostare l'oggetto metadati sull'oggetto Media Heartbeat.

      Consultate l'elenco completo dei metadati qui: Parametri [audio e video.](/help/metrics-and-metadata/audio-video-parameters.md)

   * **Metadati personalizzati -** Create un oggetto variabile per le variabili personalizzate e inserite i dati per questo contenuto.

1. **Tenere traccia dell’intenzione di avviare la riproduzione -** Per iniziare a tracciare una sessione, invocare `trackSessionStart` l’istanza di Media Heartbeat.

   >[!IMPORTANT]
   >
   >`trackSessionStart` tiene traccia delle intenzioni dell’utente in merito alla riproduzione, non dell’inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati e per stimare la metrica QoS time-to-start (la durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzate metadati personalizzati, inviate semplicemente un oggetto vuoto per l' `data` argomento in `trackSessionStart`.

1. **Tracciare l’inizio effettivo della riproduzione: identificate l’evento dal lettore multimediale per l’inizio della riproduzione, dove viene rappresentato sullo schermo il primo fotogramma del contenuto e richiamate** `trackPlay`.

1. **Tracciare il completamento della riproduzione: identificate l’evento dal lettore multimediale per il completamento della riproduzione, in cui l’utente ha guardato il contenuto fino alla fine e chiamate** `trackComplete`.

1. **Tracciare la fine della sessione** : identificate l’evento dal lettore multimediale per lo scaricamento/la chiusura della riproduzione, in cui l’utente chiude il contenuto e/o il contenuto è stato completato e scaricato e chiamate `trackSessionEnd`.

   >[!IMPORTANT]
   >
   >`trackSessionEnd` segna la fine di una sessione di tracciamento. Se la sessione è stata guardata con successo e l’utente ha guardato il contenuto fino alla fine, accertatevi che `trackComplete` venga chiamato prima `trackSessionEnd`. Qualsiasi altra chiamata `track*` API viene ignorata dopo `trackSessionEnd`, fatta eccezione per `trackSessionStart` una nuova sessione di tracciamento.

1. **Tenere traccia di tutti i possibili scenari di pausa -** Identificare l’evento dal lettore multimediale per la pausa e la chiamata `trackPause`.

   **Pausa scenari -** Identificate tutti gli scenari in cui il lettore si mette in pausa e accertatevi che `trackPause` venga chiamato correttamente. Tutti gli scenari seguenti richiedono che la chiamata dell'app `trackPause()`:

   * L'utente interrompe esplicitamente la pausa nell'app.
   * Il lettore si mette nello stato Pausa.
   * (App *mobili*) - L'utente mette l'applicazione in background, ma si desidera che l'app tenga aperta la sessione.
   * (App *mobili*) - Si verifica qualsiasi tipo di interruzione del sistema che causa il background di un'applicazione. Ad esempio, l'utente riceve una chiamata, o si verifica un pop-up da un'altra applicazione, ma si desidera che l'applicazione mantenga in vita la sessione per dare all'utente la possibilità di riprendere il contenuto dal punto di interruzione.

1. Identificare l’evento dal lettore per la riproduzione e/o per la ripresa dalla pausa e dalla chiamata `trackPlay`.

   >[!TIP]
   >
   >Può trattarsi della stessa origine evento utilizzata nel passaggio 4. Assicurati che ogni chiamata `trackPause()` API sia associata a una chiamata `trackPlay()` API seguente quando la riproduzione riprende.

1. Ascoltare gli eventi di ricerca della riproduzione dal lettore multimediale. Nella notifica dell'evento di avvio della ricerca, tenete traccia della ricerca mediante l' `SeekStart` evento.
1. Alla ricerca della notifica completa dal lettore multimediale, tenete traccia della fine della ricerca mediante l’ `SeekComplete` evento.
1. Ascoltare gli eventi di buffering della riproduzione dal lettore multimediale e, durante la notifica dell'evento di avvio del buffer, tenere traccia del buffering utilizzando l' `BufferStart` evento.
1. Nella notifica completa del buffer dal lettore multimediale, tenere traccia della fine del buffering utilizzando l' `BufferComplete` evento.

Vedi esempi di ogni passaggio negli argomenti specifici per la piattaforma riportati di seguito e guarda i lettori di esempio inclusi con i tuoi SDK.

Per un semplice esempio di tracciamento della riproduzione, consultate questo utilizzo dell’SDK JavaScript 2.x in un lettore HTML5:

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

## Convalida {#validate}

Per informazioni sulla convalida dell'implementazione, vedi [Convalida.](/help/sdk-implement/validation/validation-overview.md)

