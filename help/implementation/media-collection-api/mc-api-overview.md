---
seo-title: Overview
title: Panoramica sulle API di Streaming Media Collection
description: Scopri l’API di Media Collection e in che modo il lettore può tenere traccia degli eventi audio e video tramite le chiamate HTTP RESTful.
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
exl-id: 58430636-7fab-433a-8ead-52ccaa45d920
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 93%

---

# Panoramica sulle API di Media Collection {#overview}

L’API di Media Collection è un’alternativa RESTful di Adobe a Media SDK lato client. Con l’API di Media Collection, il lettore può tenere traccia degli eventi audio e video tramite chiamate HTTP RESTful.

L&#39;API di Media Collection è essenzialmente un adattatore che agisce come versione lato server di Media SDK. Ciò significa che alcuni aspetti della documentazione di Media SDK sono pertinenti anche per l’API di Media Collection. Ad esempio, entrambe le soluzioni utilizzano gli stessi [parametri dei contenuti multimediali in streaming](../variables/audio-video-parameters.md) e i dati di tracciamento dei contenuti multimediali in streaming raccolti determinano la stessa [generazione di report e analisi.](/help/reporting/media-reports-enable.md)

## Flussi di dati di tracciamento dei contenuti multimediali {#media-tracking-data-flows}

Un lettore multimediale che implementa l’API di Media Collection effettua chiamate di tracciamento API RESTful direttamente al server back-end di tracciamento dei contenuti multimediali, mentre un lettore che implementa Media SDK effettua chiamate di tracciamento alle API dell&#39;SDK all’interno dell’app del lettore. Un effetto dell’esecuzione di chiamate sul Web è che il lettore che implementa l’API di Media Collection deve gestire in modo automatico alcune delle elaborazioni gestite da Media SDK. (Informazioni dettagliate disponibili in [Implementazione di Media Collection.](mc-api-impl/mc-api-quick-start.md))

I dati di tracciamento acquisiti con l’API di Media Collection sono inviati e inizialmente elaborati in modo diverso rispetto ai dati di tracciamento acquisiti in un lettore di Media SDK. Tuttavia, viene utilizzato per entrambe le soluzioni lo stesso motore di elaborazione sul back-end.

![](assets/col_api_overview_simple.png)

## Panoramica API {#api-overview}

**URI:** puoi ottenerlo dal tuo rappresentante Adobe.

**Metodo HTTP:** POST, con il corpo della richiesta JSON.

### Chiamate API {#mc-api-calls}

* **`sessions`-** Stabilisce una sessione con il server e restituisce un ID sessione utilizzato in chiamate `events` successive. L’app effettua la chiamata una sola volta all’inizio di una sessione di tracciamento.

  `{uri}/api/v1/sessions`

* **`events`-** Invia i dati di tracciamento dei contenuti multimediali.

  `{uri}/api/v1/sessions/{session-id}/events`

### Corpo della richiesta {#mc-api-request-body}

```json
{
    "playerTime": {
        "playhead": "{playhead position in seconds}",
        "ts": "{timestamp in milliseconds}"
    },
    "eventType": "{event-type}",
    "params": {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    },
    "qoeData" : {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    },
    "customMetadata": {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    }
}
```

* `playerTime` - Obbligatorio per tutte le richieste.
* `eventType` - Obbligatorio per tutte le richieste.
* `params` - Obbligatorio per alcuni `eventTypes`; controlla lo [schema di convalida JSON](mc-api-ref/mc-api-json-validation.md) per determinare quali eventTypes sono obbligatori e quali facoltativi.

* `qoeData` - Facoltativo per tutte le richieste.
* `customMetadata` - Facoltativo per tutte le richieste, ma inviato solo con tipi di evento `sessionStart`, `adStart` e `chapterStart`.

Per ogni `eventType`, è presente uno [schema di convalida JSON](mc-api-ref/mc-api-json-validation.md) da utilizzare per verificare i tipi di parametro e se un parametro è facoltativo oppure obbligatorio per un particolare evento.

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
