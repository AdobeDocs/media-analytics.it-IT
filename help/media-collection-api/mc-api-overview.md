---
seo-title: Panoramica
title: Panoramica
uuid: c 14 bdbef -5846-4 d 31-8 a 14-8 e 9 e 0 e 9 c 9861
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Panoramica{#overview}

L'API Media Collection è l'alternativa restful di Adobe all'SDK lato client. Con l'API Media Collection il lettore può tenere traccia degli eventi audio e video utilizzando le chiamate a restful HTTP. L'API Media Collection offre lo stesso tracciamento tempo di Media SDK, più una funzione aggiuntiva:

* **Tracciamento dei contenuti scaricato**

   Questa funzione consente di tenere traccia dei supporti mentre un utente è offline, tramite la memorizzazione locale dei dati dell'evento fino alla restituzione online del dispositivo. (See [Track downloaded content](track-downloaded-content.md) for details.)

L'API Media Collection è essenzialmente un'adattatore che funge da versione lato server di Media SDK. Ciò significa che alcuni aspetti della documentazione di Media SDK sono pertinenti anche all'API di Media Collection. For example, both solutions use the same [Audio and Video Parameters](/help/metrics-and-metadata/audio-video-parameters.md), and the collected Audio and Video tracking data leads to the same [Reporting and Analysis.](/help/media-reports/media-reports-enable.md)

## Media Tracking Data Flows {#section_pwq_n34_qbb}

Un lettore multimediale che implementa l'API Media Collection effettua le chiamate di tracciamento API restful direttamente al server back-end di tracciamento multimediale, mentre un lettore implementa Media SDK effettua chiamate di tracciamento alle API SDK all'interno dell'app di lettore. Un effetto di esecuzione di chiamate sul Web è che il lettore implementa l'API Media Collection deve gestire parte dell'elaborazione automaticamente gestita da Media SDK. (Details in [Media Collection Implementation.](mc-api-impl/mc-api-quick-start.md))

I dati di tracciamento acquisiti con l'API Media Collection vengono inviati e inizialmente elaborati in modo diverso rispetto ai dati di tracciamento acquisiti in un lettore di Media SDK, ma lo stesso motore di elaborazione sul back-end viene utilizzato per entrambe le soluzioni.

![](assets/col_api_overview_simple.png)

## API Overview {#section_y4n_mcl_kcb}

**URI:** Ottenetelo dal rappresentante Adobe.

**Metodo HTTP:** POST, con corpo della richiesta JSON.

### API Calls {#mc-api-calls}

* **`sessions`-** Stabilisce una sessione con il server e restituisce un ID sessione utilizzato nelle `events` chiamate successive. L'app la chiama una volta all'inizio di una sessione di tracciamento.

   ```
   {uri}/api/v1/sessions
   ```

* **`events`-** Invia dati di tracciamento multimediale.

   ```
   {uri}/api/v1/sessions/{session-id}/events
   ```

### Request Body {#mc-api-request-body}

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
* `params` - Obbligatorio per alcuni `eventTypes`; controllare lo schema di convalida [JSON](mc-api-ref/mc-api-json-validation.md) per determinare quali eventtypes sono obbligatori e quali sono facoltativi.

* `qoeData` - Opzionale per tutte le richieste.
* `customMetadata` - Opzionale per tutte le richieste, ma solo per `sessionStart``adStart`i tipi di `chapterStart` evento.

For each `eventType`, there is a publicly available [JSON validation schema](mc-api-ref/mc-api-json-validation.md) that you should use to verify parameter types and whether a parameter is optional or required for a particular event.

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

