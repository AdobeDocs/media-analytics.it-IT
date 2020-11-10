---
seo-title: Panoramica
title: Panoramica
description: null
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
translation-type: tm+mt
source-git-commit: fdec4da99a43d889690638f1ff3579e145548b69
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 1%

---


# Panoramica{#overview}

L&#39;API Media Collection è  Adobe  alternativa RESTful all&#39;SDK multimediale lato client. Con l’API Media Collection, il lettore può tenere traccia degli eventi audio e video mediante chiamate RESTful HTTP.

L&#39;API Media Collection è essenzialmente una scheda che agisce come una versione lato server dell&#39;SDK Media. Ciò significa che alcuni aspetti della documentazione di Media SDK sono pertinenti anche per l&#39;API di Media Collection. Ad esempio, entrambe le soluzioni utilizzano lo stesso [Parametri dei supporti di streaming](/help/metrics-and-metadata/audio-video-parameters.md)e i dati raccolti per il tracciamento dei supporti di vapore portano allo stesso [Reporting and Analysis.](/help/media-reports/media-reports-enable.md)

## Flussi dati di tracciamento file multimediali {#media-tracking-data-flows}

Un lettore multimediale che implementa l’API Media Collection effettua chiamate RESTful di tracciamento API direttamente al server back-end di tracciamento dei contenuti multimediali, mentre un lettore che implementa l’SDK di Media effettua chiamate di tracciamento alle API SDK all’interno dell’app lettore. Uno degli effetti delle chiamate sul Web è che il lettore che implementa l’API di Media Collection deve gestire in modo automatico alcune delle elaborazioni gestite dall’SDK di Media. (Dettagli in [Implementazione di Media Collection.](mc-api-impl/mc-api-quick-start.md))

I dati di tracciamento acquisiti con l’API Media Collection vengono inviati e inizialmente elaborati in modo diverso rispetto ai dati di tracciamento acquisiti in un lettore SDK Media, ma lo stesso motore di elaborazione sul back-end viene utilizzato per entrambe le soluzioni.

![](assets/col_api_overview_simple.png)

## Panoramica API {#api-overview}

**URI:** Ottenete questo risultato dal rappresentante  Adobe.

**Metodo HTTP:** POST, con il corpo della richiesta JSON.

### Chiamate API {#mc-api-calls}

* **`sessions`-** Stabilisce una sessione con il server e restituisce un ID sessione utilizzato in `events` chiamate. L’app esegue questa chiamata una volta all’inizio di una sessione di tracciamento.

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
* `params` - Obbligatorio per alcuni `eventTypes`; controllare [Schema di convalida JSON](mc-api-ref/mc-api-json-validation.md) per determinare quali eventTypes sono obbligatori e quali sono facoltativi.

* `qoeData` - Facoltativo per tutte le richieste.
* `customMetadata` - Facoltativo per tutte le richieste, ma solo inviato con `sessionStart`, `adStart`, and `chapterStart` tipi di evento.

Per ogni `eventType`, esiste un [Schema di convalida JSON](mc-api-ref/mc-api-json-validation.md) utilizzate per verificare i tipi di parametri e se un parametro è facoltativo o obbligatorio per un particolare evento.

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
