---
title: Spiegazione del tracciamento della riproduzione dei contenuti
description: '"Scopri come tracciare la riproduzione core, compresi il caricamento dei file multimediali, l’avvio dei file multimediali, la pausa dei file multimediali e il completamento dei file multimediali. "'
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 2%

---

# Panoramica del tracciamento{#tracking-overview}

>[!IMPORTANT]
>
>Questa documentazione tratta il tracciamento nella versione 2.x dell&#39;SDK. Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Eventi del lettore

Il tracciamento della riproduzione di base include il tracciamento del caricamento dei file multimediali, l&#39;avvio dei file multimediali, la pausa dei file multimediali e il completamento dei file multimediali. Sebbene non sia obbligatorio, il tracciamento del buffering e della ricerca sono anche componenti core utilizzati per il tracciamento della riproduzione dei contenuti. Nell’API del lettore multimediale, identifica gli eventi del lettore corrispondenti alle chiamate di tracciamento Media SDK e codifica i gestori di eventi per chiamare le API di tracciamento e per popolare le variabili richieste e facoltative.

### Al caricamento del supporto

* Creare l&#39;oggetto multimediale
* Compilare metadati
* Chiama `trackSessionStart`; Ad esempio: `trackSessionStart(mediaObject, contextData)`

### All&#39;avvio del supporto

* Chiamata `trackPlay`

### In pausa/ripresa

* Chiamata `trackPause`
* Chiama `trackPlay`   _quando la riproduzione riprende_

### Supporto completo

* Chiamata `trackComplete`

### In caso di interruzione del contenuto multimediale

* Chiamata `trackSessionEnd`

### Quando inizia lo scorrimento

* Chiamata `trackEvent(SeekStart)`

### Quando la pulizia termina

* Chiamata `trackEvent(SeekComplete)`

### Quando inizia il buffering

* Chiamata `trackEvent(BufferStart);`

### Quando il buffering termina

* Chiamata `trackEvent(BufferComplete);`

>[!TIP]
>
>La posizione della testina di riproduzione viene impostata come parte del codice di configurazione e configurazione. Per ulteriori informazioni su `getCurrentPlayheadTime`, consulta [Panoramica: Linee guida generali sull&#39;implementazione.](/help/sdk-implement/setup/setup-overview.md#general-implementation-guidelines)

## Implementazione {#implement}

1. **Configurazione del tracciamento iniziale:** identifica quando l’utente attiva l’intenzione di riproduzione (l’utente fa clic su Play e/o autoplay è attivato) e crea un’ `MediaObject` istanza utilizzando le informazioni sul contenuto multimediale per nome, ID contenuto, lunghezza del contenuto e tipo di flusso.

   **`MediaObject`riferimento:**

   | Nome variable | Descrizione | Obbligatorio |
   |---|---|---|
   | `name` | Nome del contenuto | Sì |
   | `mediaid` | Identificatore univoco del contenuto | Sì |
   | `length` | Lunghezza del contenuto | Sì |
   | `streamType` | Tipo di flusso | Sì |
   | `mediaType` | Tipo di supporto (contenuto audio o video) | Sì |

   **`StreamType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `VOD` | Tipo di flusso per Video on Demand. |
   | `LIVE` | Tipo di flusso per il contenuto live. |
   | `LINEAR` | Tipo di flusso per il contenuto lineare. |
   | `AOD` | Tipo di flusso per audio su richiesta |
   | `AUDIOBOOK` | Tipo di flusso per la rubrica audio |
   | `PODCAST` | Tipo di flusso per Podcast |

   **`MediaType`costanti:**

   | Nome costante | Descrizione |
   |---|---|
   | `Audio` | Tipo di supporto per flussi audio. |
   | `Video` | Tipo di supporto per i flussi video. |

   Il formato generale per la creazione di `MediaObject` è `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **Allega metadati:** è possibile allegare oggetti metadati standard e/o personalizzati alla sessione di tracciamento tramite variabili di dati di contesto.

   * **Metadati standard -**

      >[!NOTE]
      >
      >Il collegamento dell&#39;oggetto metadati standard all&#39;oggetto multimediale è facoltativo.

      Creare un&#39;istanza di un oggetto metdata standard, compilare le variabili desiderate e impostare l&#39;oggetto metadati sull&#39;oggetto Media Heartbeat.

      Vedi l&#39;elenco completo dei metadati qui: [Parametri audio e video.](/help/metrics-and-metadata/audio-video-parameters.md)

   * **Metadati personalizzati -** Crea un oggetto variabile per le variabili personalizzate e compila i dati per questo contenuto.

1. **Tracciare l&#39;intenzione di avviare la riproduzione -** Per iniziare a tracciare una sessione, invoca  `trackSessionStart` l&#39;istanza Media Heartbeat.

   >[!IMPORTANT]
   >
   >`trackSessionStart` tiene traccia delle intenzioni dell&#39;utente in merito alla riproduzione, non dell&#39;inizio della riproduzione. Questa API viene utilizzata per caricare i dati/metadati e per stimare la metrica QoS time-to-start (la durata tra `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se non utilizzi metadati personalizzati, invia semplicemente un oggetto vuoto per l’argomento `data` in `trackSessionStart`.

1. **Tracciare l’inizio effettivo della riproduzione:** identifica l’evento dal lettore multimediale per l’inizio della riproduzione, in cui viene eseguito il rendering del primo fotogramma del contenuto sullo schermo e chiama  `trackPlay`.

1. **Tracciare il completamento della riproduzione:** identifica l’evento dal lettore multimediale per il completamento della riproduzione, dove l’utente ha guardato il contenuto fino alla fine, e chiama  `trackComplete`.

1. **Traccia la fine della sessione -** Identifica l’evento dal lettore multimediale per lo scaricamento/la chiusura della riproduzione, in cui l’utente chiude il contenuto e/o il contenuto viene completato e scaricato e chiama  `trackSessionEnd`.

   >[!IMPORTANT]
   >
   >`trackSessionEnd` segna la fine di una sessione di tracciamento. Se la sessione è stata controllata correttamente al completamento, dove l’utente ha guardato il contenuto fino alla fine, assicurati che `trackComplete` venga chiamato prima di `trackSessionEnd`. Qualsiasi altra chiamata API `track*` viene ignorata dopo `trackSessionEnd`, tranne `trackSessionStart` per una nuova sessione di tracciamento.

1. **Tracciare tutti i possibili scenari di pausa:** identifica l’evento dal lettore multimediale per la pausa e la chiamata  `trackPause`.

   **Pausa scenari:** identifica qualsiasi scenario in cui il lettore si mette in pausa e assicurati che  `trackPause` venga chiamato correttamente. I seguenti scenari richiedono tutti che la chiamata all&#39;app `trackPause()`:

   * L’utente inserisce esplicitamente una pausa nell’app.
   * Il lettore si mette in stato di Pausa.
   * (*App mobili*) - L&#39;utente mette l&#39;applicazione in background, ma desideri che l&#39;app mantenga aperta la sessione.
   * (*App mobili*) - Si verifica un qualsiasi tipo di interruzione del sistema che causa lo sfondo di un&#39;applicazione. Ad esempio, l’utente riceve una chiamata, o si verifica un pop-up da un’altra applicazione, ma si desidera che l’applicazione mantenga in vita la sessione per dare all’utente la possibilità di riprendere il contenuto dal punto di interruzione.

1. Identifica l&#39;evento dal lettore per la riproduzione e/o la ripresa dalla pausa e chiama `trackPlay`.

   >[!TIP]
   >
   >Può trattarsi della stessa origine evento utilizzata nel passaggio 4. Assicurati che ogni chiamata API `trackPause()` sia associata a una seguente chiamata API `trackPlay()` quando la riproduzione riprende.

1. Ascoltare gli eventi di ricerca della riproduzione dal lettore multimediale. Nella notifica dell&#39;evento di ricerca start, tieni traccia della ricerca utilizzando l&#39;evento `SeekStart` .
1. Al momento della ricerca della notifica completa da parte del lettore multimediale, tieni traccia della fine della ricerca utilizzando l&#39;evento `SeekComplete` .
1. Ascolta gli eventi di buffering di riproduzione dal lettore multimediale e, in caso di notifica dell&#39;evento di avvio del buffer, tieni traccia del buffering utilizzando l&#39;evento `BufferStart` .
1. Al momento della notifica completa del buffer da parte del lettore multimediale, tieni traccia della fine del buffering utilizzando l&#39;evento `BufferComplete` .

Vedi esempi di ogni passaggio negli argomenti specifici per la piattaforma seguenti e osserva i lettori di esempio inclusi negli SDK.

Per un semplice esempio di tracciamento della riproduzione, consulta questo utilizzo dell’SDK JavaScript 2.x in un lettore HTML5:

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

Per informazioni sulla convalida dell&#39;implementazione, consulta [Convalida.](/help/sdk-implement/validation/validation-overview.md)
