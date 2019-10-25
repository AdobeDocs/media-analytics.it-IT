---
seo-title: Panoramica
title: Panoramica
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# Panoramica{#overview}

L’API Media Collection è l’alternativa REST di Adobe all’SDK per file multimediali lato client. Con l’API Media Collection, il lettore può tenere traccia degli eventi audio e video mediante chiamate RESTful HTTP. L’API Media Collection offre lo stesso tracciamento in tempo reale dell’SDK per file multimediali, più una funzione aggiuntiva:

* **Tracciamento del contenuto scaricato**

   Questa funzione consente di tenere traccia dei contenuti multimediali mentre un utente è offline, memorizzando i dati dell'evento in locale fino a quando il dispositivo dell'utente non torna online. (Per informazioni dettagliate, consultate [Tenere traccia del contenuto](track-downloaded-content.md) scaricato.)

L'API Media Collection è essenzialmente una scheda che agisce come una versione lato server dell'SDK Media. Ciò significa che alcuni aspetti della documentazione di Media SDK sono pertinenti anche per l'API di Media Collection. Ad esempio, entrambe le soluzioni utilizzano gli stessi parametri [](/help/metrics-and-metadata/audio-video-parameters.md)[audio e video, mentre i dati di tracciamento audio e video raccolti portano allo stesso reporting e analisi.](/help/media-reports/media-reports-enable.md)

## Flussi dati di tracciamento file multimediali {#media-tracking-data-flows}

Un lettore multimediale che implementa l’API Media Collection effettua chiamate RESTful di tracciamento API direttamente al server back-end di tracciamento dei contenuti multimediali, mentre un lettore che implementa l’SDK di Media effettua chiamate di tracciamento alle API SDK all’interno dell’app lettore. Uno degli effetti delle chiamate sul Web è che il lettore che implementa l’API di Media Collection deve gestire in modo automatico alcune delle elaborazioni gestite dall’SDK di Media. (Dettagli nell’implementazione di [Media Collection.](mc-api-impl/mc-api-quick-start.md))

I dati di tracciamento acquisiti con l’API Media Collection vengono inviati e inizialmente elaborati in modo diverso rispetto ai dati di tracciamento acquisiti in un lettore SDK Media, ma lo stesso motore di elaborazione sul back-end viene utilizzato per entrambe le soluzioni.

![](assets/col_api_overview_simple.png)

## Panoramica API {#api-overview}

**** URI: Ottenete questo risultato dal rappresentante Adobe.

**** Metodo HTTP: POST, con il corpo della richiesta JSON.

### Chiamate API {#mc-api-calls}

* **`sessions`-** Stabilisce una sessione con il server e restituisce un ID sessione utilizzato nelle `events` chiamate successive. L’app esegue questa chiamata una volta all’inizio di una sessione di tracciamento.

   ```
   {uri}/api/v1/sessions
   ```

* **`events`-** Invia i dati di tracciamento dei supporti.

   ```
   {uri}/api/v1/sessions/{session-id}/events
   ```

### Corpo della richiesta {#mc-api-request-body}

```
{ 
    "playerTime": { 
        "playhead": {playhead position in seconds}, 
        "ts": {timestamp in milliseconds} 
    }, 
    "eventType": {event-type}, 
    "params": { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    }, 
    "qoeData" : { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    }, 
    "customMetadata": { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    } 
} 
```

* `playerTime` - Obbligatorio per tutte le richieste.
* `eventType` - Obbligatorio per tutte le richieste.
* `params` - Obbligatorio per alcuni `eventTypes`; controllare lo schema [di convalida](mc-api-ref/mc-api-json-validation.md) JSON per determinare quali eventTypes sono obbligatori e quali sono facoltativi.

* `qoeData` - Facoltativo per tutte le richieste.
* `customMetadata` - Facoltativo per tutte le richieste, ma solo inviato con `sessionStart`, `adStart`e i tipi di `chapterStart` evento.

Per ciascun `eventType`oggetto è disponibile al pubblico uno schema [di convalida](mc-api-ref/mc-api-json-validation.md) JSON da utilizzare per verificare i tipi di parametro e se un parametro è facoltativo o obbligatorio per un particolare evento.

### Tipi di evento {#mc-api-event-types}

* `sessionStart`
* `play`
* `ping`
* `pauseStart`
* `bufferStart`
* `adStart`
* `adComplete`
* `adSkip`
* `adBreakStart`
* `adBreakComplete`
* `chapterStart`
* `chapterSkip`
* `chapterComplete`
* `sessionEnd`
* `sessionComplete`

