---
title: Informazioni sulle timeline di tracciamento del contenuti multimediale - L’utente abbandona la sessione
description: Scopri la timeline dell’indicatore di riproduzione e la corrispondente azione dell’utente quando una sessione video viene abbandonata. Scopri i dettagli di ogni azione e richiesta.
uuid: 74b89e8f-ef56-4e0c-b9a8-40739e15b4cf
exl-id: 0c6a89f4-7949-4623-8ed9-ce1d1547bdfa
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4c68f5997a9d336e8c3545cdfb7b9cb955602b69
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 100%

---

# Timeline 2: utente abbandona la sessione {#timeline--2-user-abandons-session}

## VOD, annunci pre-roll e mid-roll, l’utente abbandona i contenuti in anticipo

I seguenti diagrammi illustrano la tempistica della testina di riproduzione e la corrispondenza con le azioni di un utente. Di seguito sono riportati i dettagli di ciascuna azione e le relative richieste.

![Contenuto API](assets/va_api_content_2.png)

![Azioni API](assets/va_api_actions_2.png)

## Dettagli azione

### Azione 1 - Avvia sessione {#Action-1}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Pulsante di riproduzione o riproduzione automatica premuto | 0 | 0 | `/api/v1/sessions` |

Questa chiamata segnala _l’intenzione dell’utente di riprodurre_ un video. Restituisce un ID sessione (`{sid}`) al client utilizzato per identificare tutte le chiamate di tracciamento successive all’interno della sessione. Lo stato del lettore non è ancora “in riproduzione”, ma è “in avvio”. I parametri di sessione obbligatori devono essere inclusi nella mappa `params` nel corpo della richiesta.  Nel backend, questa chiamata genera una chiamata di avvio Adobe Analytics. Per informazioni sulle sessioni, consulta la documentazione delle API di Media Collection.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "sessionStart",
    "params": {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR-TS_ ]",
        "analytics.reportSuite": "[ _YOUR-RSID_ ]",
        "analytics.visitorId": "[ _YOUR-VISITOR-ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR-MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### Azione 2 - Avvio timer del ping {#Action-2}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app avvia il timer dell’evento ping | 0 | 0 | |

Avvia il timer ping dell’app. Il primo evento ping dovrebbe quindi attivarsi in 1 secondo se ci sono annunci pre-roll, 10 secondi in caso contrario.

### Azione 3 - Avvio dell’interruzione pubblicitaria {#Action-3}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento inizio dell’interruzione pubblicitaria pre-roll | 0 | 0 | `/api/v1/sessions/{sid}/events` |

Gli annunci pre-roll devono essere tracciati. Gli annunci possono essere tracciati solo all’interno di un’interruzione pubblicitaria.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0,
        "media.ad.podSecond": 0
    }
}
```

### Azione 4 - Avvio dell’annuncio {#Action-4}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento dell’inizio dell’annuncio pre-roll n.1 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

Inizia un annuncio di 12 secondi.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz-creative.com",
        "media.ad.placementId": "sample-placement2"
    },
}
```

### Azione 5: ping annuncio {#Action-5}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 1 | 0 | `/api/v1/sessions/{sid}/events` |

Esegui il ping del backend ogni 1 secondo. (I successivi ping degli annunci non vengono visualizzati per brevità.)

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Azione 6 - Annuncio completato {#Action-6}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Traccia il completamento del 1° annuncio pre-roll | 12 | 0 | `/api/v1/sessions/{sid}/events` |

Il primo annuncio pre-roll è finito.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### Azione 7: pausa annuncio completata {#Action-7}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento dell’annuncio pre-roll completato | 12 | 0 | `/api/v1/sessions/{sid}/events` |

L’interruzione pubblicitaria è terminata. Durante la pausa annuncio, il lettore è rimasto in stato di “riproduzione”.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakComplete"
}
```

### Azione 8: riproduzione contenuto {#Action-8}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento dell’evento di riproduzione | 12 | 0 | `/api/v1/sessions/{sid}/events` |

Sposta il lettore sullo stato di “riproduzione”; inizia il tracciamento dell’avvio della riproduzione del contenuto.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "play",
    "qoeData": {
        "bitrate": 10000
    }
}
```

### Azione 9: ping {#Action-9}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 20 | 8 | `/api/v1/sessions/{sid}/events` |

Esegui il ping del backend ogni 10 secondi.

```json
{
    "playerTime": {
        "playhead": 8,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Azione 10: ping {#Action-10}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 30 | 18 | `/api/v1/sessions/{sid}/events` |

Esegui il ping del backend ogni 10 secondi.

```json
{
    "playerTime": {
        "playhead": 18,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Azione 11: errore {#Action-11}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Si verifica un errore, l’app invia informazioni sull’errore. | 32 | 20 | `/api/v1/sessions/{sid}/events` |

```json
{
    "playerTime": {
        "playhead": 20,
        "ts": "<timestamp>"
    },
    "eventType": "error"
}
```

### Azione 12: riproduzione del contenuto {#Action-12}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app si ripristina dopo l’errore, l’utente preme Riproduci | 37 | 20 | `/api/v1/sessions/{sid}/events` |

```json
{
    "playerTime": {
        "playhead": 18,
        "ts": "<timestamp>"
    },
    "eventType":"play",
    "qoeData": {
        "bitrate": 10000
    }
}
```

### Azione 13: ping {#Action-13}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 40 | 28 | `/api/v1/sessions/{sid}/events` |

Esegui il ping del backend ogni 10 secondi.

```json
{
    "playerTime": {
        "playhead": 28,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Azione 14: avvio dell’interruzione dell’annuncio {#Action-14}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento avvio interruzione pubblicitaria mid-roll | 45 | 33 | `/api/v1/sessions/{sid}/events` |

Annuncio mid-roll con una durata di 8 secondi: invia `adBreakStart`.

```json
{
    "playerTime": {
        "playhead": 33,
        "ts": "<timestamp>"
    },
    "eventType":"adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 33
    }
}
```

### Azione 15: avvio dell’annuncio {#Action-15}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Avvio tracciamento annuncio mid-roll n.1 | 45 | 33 | `/api/v1/sessions/{sid}/events` |

Tracciamento dell’annuncio mid-roll.

```json
{
    "playerTime": { "playhead": 33, "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 8,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "7",
        "media.ad.creativeId": "40",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://example.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Azione 16: chiusura dell’app {#Action-16}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’utente chiude l’app. L’app determina che l’utente ha abbandonato la visualizzazione e non ritorna alla sessione. | 48 | 33 | `/api/v1/sessions/{sid}/events` |

Invia `sessionEnd` al backend VA per indicare che la sessione deve essere chiusa immediatamente, senza ulteriore elaborazione.

```json
{
    "playerTime": {
        "playhead": 33,
        "ts": "<timestamp>"
    },
    "eventType": "sessionEnd"
}
```
