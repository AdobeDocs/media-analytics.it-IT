---
seo-title: Overview
title: Panoramica sulle API di Streaming Media Collection
description: Scopri l’API di Media Collection e in che modo il lettore può tenere traccia degli eventi audio e video tramite le chiamate HTTP RESTful.
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
exl-id: 58430636-7fab-433a-8ead-52ccaa45d920
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/79XLYzuvi3neUuCrt3LcGEwnnaR038-mWHMuSrY797M
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 347
ht-degree: 91%

---

# Panoramica sulle API di Media Collection {#overview}

L’API di Media Collection è un’alternativa RESTful di Adobe a Media SDK lato client. Con l’API di Media Collection, il lettore può tenere traccia degli eventi audio e video tramite chiamate HTTP RESTful.

L&#39;API di Media Collection è essenzialmente un adattatore che agisce come versione lato server di Media SDK. I dati di tracciamento dei contenuti multimediali in streaming raccolti determinano lo stesso [Reporting and Analysis](/help/reporting/setup/analytics-reporting.md).

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

Per l&#39;elenco completo dei tipi di evento con esempi di implementazione per SDK, vedere [Panoramica eventi](/help/implementation/events/overview.md).
