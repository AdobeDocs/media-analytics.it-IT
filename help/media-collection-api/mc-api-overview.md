---
seo-title: Panoramica
title: Panoramica API Streaming Media Collection
description: Scopri l’API Media Collection e come il lettore può tenere traccia degli eventi audio e video utilizzando le chiamate RESTful HTTP.
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
exl-id: 58430636-7fab-433a-8ead-52ccaa45d920
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%

---

# Panoramica{#overview}

L’API Media Collection è un’alternativa RESTful di Adobe all’SDK Media lato client. Con l’API Media Collection, il lettore può tenere traccia degli eventi audio e video utilizzando chiamate RESTful HTTP.

L&#39;API Media Collection è essenzialmente un adattatore che agisce come versione lato server dell&#39;SDK Media. Ciò significa che alcuni aspetti della documentazione Media SDK sono pertinenti anche all’API Media Collection. Ad esempio, entrambe le soluzioni utilizzano gli stessi [parametri multimediali in streaming](/help/metrics-and-metadata/audio-video-parameters.md) e i dati di tracciamento dei file multimediali in streaming raccolti portano allo stesso [Reporting and Analysis.](/help/media-reports/media-reports-enable.md)

## Flussi di dati di tracciamento dei file multimediali {#media-tracking-data-flows}

Un lettore multimediale che implementa l’API Media Collection effettua chiamate di tracciamento RESTful API direttamente al server back-end di tracciamento dei contenuti multimediali, mentre un lettore che implementa l’SDK Media effettua chiamate di tracciamento alle API SDK all’interno dell’app di lettore. Un effetto dell’esecuzione di chiamate sul web è che il lettore che implementa l’API Media Collection deve gestire in modo automatico alcune delle elaborazioni gestite dall’SDK Media. (Dettagli in [Implementazione di Media Collection.](mc-api-impl/mc-api-quick-start.md))

I dati di tracciamento acquisiti con l’API Media Collection vengono inviati e inizialmente elaborati in modo diverso rispetto ai dati di tracciamento acquisiti in un lettore Media SDK, ma lo stesso motore di elaborazione sul back-end viene utilizzato per entrambe le soluzioni.

![](assets/col_api_overview_simple.png)

## Panoramica API {#api-overview}

**URI:** recupera questo messaggio dal rappresentante di Adobe.

**Metodo HTTP:** POST, con il corpo della richiesta JSON.

### Chiamate API {#mc-api-calls}

* **`sessions`-** Stabilisce una sessione con il server e restituisce un ID sessione utilizzato nelle  `events` chiamate successive. L’app la chiama una volta all’inizio di una sessione di tracciamento.

   ```
   {uri}/api/v1/sessions
   ```

* **`events`-** invia i dati di tracciamento dei contenuti multimediali.

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
* `params` - Obbligatorio per alcuni  `eventTypes`; controlla lo  [schema di convalida ](mc-api-ref/mc-api-json-validation.md) JSON per determinare quali tipi di evento sono obbligatori e quali sono facoltativi.

* `qoeData` - Facoltativo per tutte le richieste.
* `customMetadata` - Facoltativo per tutte le richieste, ma solo per i tipi di  `sessionStart`,  `adStart` e  `chapterStart` evento.

Per ogni `eventType`, è disponibile al pubblico [Schema di convalida JSON](mc-api-ref/mc-api-json-validation.md) da utilizzare per verificare i tipi di parametro e se un parametro è facoltativo o obbligatorio per un particolare evento.

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
