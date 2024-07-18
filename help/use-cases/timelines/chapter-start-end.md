---
title: Cos’è la timeline di inizio e fine del capitolo multimediale in streaming
description: Scopri le tempistiche della testina di riproduzione e quando inizia e termina un capitolo.
uuid: 41b52072-e1cd-4dda-9253-31f3408924f6
exl-id: e3f5bbdb-7007-435b-920c-566d163e57ad
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 100%

---

# Timeline: Capitoli {#timeline-3-chapters}

## VOD, annunci pre-roll, pausa, buffering, visualizzazione del contenuto fino alla fine

I seguenti diagrammi illustrano la tempistica della testina di riproduzione e la corrispondenza con le azioni di un utente. Di seguito sono riportati i dettagli di ciascuna azione e le relative richieste.

![Contenuto API](assets/va_api_content_3.png)

![Azioni API](assets/va_api_actions_3.png)

## Dettagli azione

### Azione 1 - Avvia sessione {#Action-1}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Premendo il pulsante Riproduzione automatica o Riproduzione, il video inizia a caricarsi. | 0 | 0 | `/api/v1/sessions` |

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
        "analytics.reportSuite": "[ _YOUR_RSID_ ]",
        "analytics.visitorId": "[ _YOUR_VISITOR_ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR_MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### Azione 2: avvio del timer di ping {#Action-2}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app avvia il timer dell’evento ping | 0 | 0 | |

Avvia il timer di ping. Il primo evento ping dovrebbe quindi attivarsi in 1 secondo se ci sono annunci pre-roll, 10 secondi in caso contrario.

### Azione 3 - Avvio dell’interruzione pubblicitaria {#Action-3}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento inizio dell’interruzione pubblicitaria pre-roll | 0 | 0 | `/api/v1/sessions/{sid}/events` |

Gli annunci possono essere tracciati solo all’interno di un’interruzione pubblicitaria.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0, "media.ad.podSecond": 0
    }
}
```

### Azione 4 - Avvio dell’annuncio {#Action-4}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento dell’inizio dell’annuncio pre-roll n.1 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

Inizia il tracciamento del primo annuncio pre-roll, che è lungo 15 secondi. Inclusione di metadati personalizzati con questo `adStart`.

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
        "media.ad.id": "001",
        "media.ad.length": 15,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://example.com",
        "media.ad.placementId": "sample_placement"
    },
    "customMetadata": {
        "myCustomData1": "CustomData1",
        "myCustomData2": "CustomData2"
    }
}
```

### Azione 5: ping annuncio {#Action-5}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 10 | 0 | `/api/v1/sessions/{sid}/events` |

Esegui il ping del backend ogni 1 secondo. I ping di annuncio successivi non vengono visualizzati per brevità.

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
| Traccia il completamento del 1° annuncio pre-roll | 15 | 0 | `/api/v1/sessions/{sid}/events` |

Traccia la fine del primo annuncio pre-roll.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### Azione 7 - Avvio dell’annuncio {#Action-7}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Traccia l’inizio del 2° annuncio pre-roll | 15 | 0 | `/api/v1/sessions/{sid}/events` |

Traccia l’inizio del secondo annuncio pre-roll, che ha una durata di 7 secondi.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 2",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "2",
        "media.ad.creativeId": "44",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://example.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Azione 8 - Ping dell’annuncio {#Action-8}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 16 | 0 | `/api/v1/sessions/{sid}/events` |

Esegui il ping del backend ogni 1 secondo. I ping di annuncio successivi non vengono visualizzati per brevità.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Azione 9 - Annuncio completato {#Action-9}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Traccia il completamento del 2° annuncio pre-roll | 22 | 0 | `/api/v1/sessions/{sid}/events` |

Traccia la fine del secondo annuncio pre-roll.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### Azione 10 - Completamento dell’interruzione pubblicitaria {#Action-10}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento dell’annuncio pre-roll completato | 22 | 0 | `/api/v1/sessions/{sid}/events` |

L’interruzione pubblicitaria è terminata. Durante l’interruzione pubblicitaria, lo stato della riproduzione è rimasto “in esecuzione”.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakComplete"
}
```

### Azione 11 - Riproduci il contenuto {#Action-11}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento dell’evento di riproduzione | 22 | 0 | `/api/v1/sessions/{sid}/events` |

Dopo l’evento `adBreakComplete`, imposta il lettore nello stato di “riproduzione” utilizzando l’evento `play`.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "play"
}
```

### Azione 12: inizio capitolo {#Action-12}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Traccia evento di inizio capitolo | 23 | 1 | `/api/v1/sessions/{sid}/events` |

Dopo l’evento di riproduzione, traccia l’inizio del primo capitolo.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "chapterStart",
    "params": {
        "media.chapter.index": 1,
        "media.chapter.offset": 0, "media.chapter.length": 20, "media.chapter.friendlyName": "Chapter Uno"
    },
}
```

### Azione 13: ping {#Action-13}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 30 | 8 | `/api/v1/sessions/{sid}/events` |

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

### Azione 14: avvio del buffer {#Action-14}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Si è verificato un evento di avvio del buffer | 33 | 11 | `/api/v1/sessions/{sid}/events` |

Traccia lo spostamento allo stato di “buffering”.

```json
{
    "playerTime": {
        "playhead": 11,
        "ts": "<timestamp>"
    },
    "eventType": "bufferStart"
}
```

### Azione 15: fine buffer (riproduzione) {#Action-15}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Buffering terminato, l’app tiene traccia della ripresa del contenuto | 36 | 11 | `/api/v1/sessions/{sid}/events` |

Il buffering termina dopo 3 secondi, quindi riporta il lettore allo stato di “riproduzione”. Devi inviare un altro evento di riproduzione del tracciamento proveniente dal buffering. **La chiamata `play` dopo `bufferStart` implica una chiamata “bufferEnd” al back-end,** quindi non è necessario un evento `bufferEnd`.

```json
{
    "playerTime": {
        "playhead": 11,
        "ts": "<timestamp>"
    },
    "eventType": "play"
}
```

### Azione 16: ping {#Action-16}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 40 | 15 | `/api/v1/sessions/{sid}/events` |

Esegui il ping del backend ogni 10 secondi.

```json
{
    "playerTime": {
        "playhead": 15,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Azione 17: fine capitolo {#Action-17}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app traccia la fine del capitolo | 45 | 20 | `/api/v1/sessions/{sid}/events` |

Il primo capitolo termina subito prima della seconda interruzione pubblicitaria.

```json
{
    "playerTime": {
        "playhead": 20,
        "ts": "<timestamp>"
    },
    "eventType": "chapterComplete"
}
```

### Azione 18: avvio interruzione pubblicitaria {#Action-18}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento avvio interruzione pubblicitaria mid-roll | 46 | 21 | `/api/v1/sessions/{sid}/events` |

Annuncio mid-roll con una durata di 8 secondi: invia `adBreakStart`.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1, "media.ad.podSecond": 21
    }
}
```

### Azione 19: inizio annuncio {#Action-19}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento avvio dell’annuncio mid-roll n.3 | 46 | 21 | `/api/v1/sessions/{sid}/events` |

Tracciamento dell’annuncio mid-roll.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.name": "Ad 3",
        "media.ad.id": "003",
        "media.ad.length": 8,
        "media.ad.podPosition": 2,
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

### Azione 20: ping annuncio {#Action-20}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 47 | 21 | `/api/v1/sessions/{sid}/events` |

Esegui il ping del backend ogni 1 secondo. I ping di annuncio successivi non vengono visualizzati per brevità.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Azione 21: annuncio completo {#Action-21}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento annuncio mid-roll n.1 completato | 54 | 21 | `/api/v1/sessions/{sid}/events` |

L’annuncio mid-roll è completo.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### Azione 22: interruzione annuncio completata {#Action-22}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento interruzione pubblicitaria mid-roll completato | 54 | 21 | `/api/v1/sessions/{sid}/events` |

L’interruzione pubblicitaria è stata completata.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakComplete"
}
```

### Azione 23: inizio capitolo {#Action-23}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Traccia l’inizio del capitolo 2 | 55 | 22 | `/api/v1/sessions/{sid}/events` |



```json
{
    "playerTime": {
        "playhead": 22,
        "ts": "<timestamp>"
    },
    "eventType": "chapterStart",
    "params": {
        "media.chapter.index": 2,
        "media.chapter.offset": 22, "media.chapter.length": 22, "media.chapter.friendlyName": "Chapter Dos"
    },
}
```

### Azione 24: ping {#Action-24}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 60 | 27 | `/api/v1/sessions/{sid}/events` |

Esegui il ping del backend ogni 10 secondi.

```json
{
    "playerTime": {
        "playhead": 27,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Azione 25: pausa {#Action-25}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’utente ha premuto pausa | 64 | 31 | `/api/v1/sessions/{sid}/events` |

L’azione dell’utente sposta lo stato di riproduzione su “messo in pausa”.

```json
{
    "playerTime": {
        "playhead": 31,
        "ts": "<timestamp>"
    },
    "eventType": "pauseStart"
}
```

### Azione 26: ping {#Action-26}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 70 | 31 | `/api/v1/sessions/{sid}/events` |

Esegui il ping del backend ogni 10 secondi. Il lettore è ancora in stato di “buffering”; l’utente rimane bloccato a 20 secondi di contenuto. Furente...

```json
{
    "playerTime": {
        "playhead": 31,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Azione 27: riprodurre il contenuto {#Action-27}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’utente ha premuto Play per riprendere il contenuto principale | 74 | 31 | `/api/v1/sessions/{sid}/events` |

Sposta lo stato di riproduzione su “in riproduzione”.  **La chiamata `play` dopo `pauseStart` implica una chiamata “riprendi” al back end**, quindi non è necessario un evento `resume`.

```json
{
    "playerTime": {
        "playhead": 31,
        "ts": "<timestamp>"
    },
    "eventType": "play"
}
```

### Azione 28: ping {#Action-28}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 80 | 37 | `/api/v1/sessions/{sid}/events` |

Esegui il ping del backend ogni 10 secondi.

```json
{
    "playerTime": {
        "playhead": 37,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Azione 29: fine capitolo {#Action-29}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Fine capitolo 2 | 87 | 44 | `/api/v1/sessions/{sid}/events` |

Traccia la fine del secondo e ultimo capitolo.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "chapterComplete"
}
```

### Azione 30: sessione completa {#Action-30}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’utente termina di guardare il contenuto fino alla fine. | 88 | 45 | `/api/v1/sessions/{sid}/events` |

Invia `sessionComplete` al backend per indicare che l’utente ha terminato di guardare l’intero contenuto.

```json
{
    "playerTime": {
        "playhead": 45,
        "ts": "<timestamp>"
    },
    "eventType": "sessionComplete"
}
```


>[!NOTE]
>
>**Nessun evento di ricerca? -** Non è disponibile alcun supporto esplicito nell’API di Media Collection per eventi `seekStart` o `seekComplete`. Alcuni utenti generano un numero molto elevato di tali eventi nel momento in cui l’utente finale esegue la pulizia. Inoltre, è probabile che le diverse centinaia di utenti causino un bottleneck della larghezza di banda di un servizio back-end. Adobe si basa su un supporto esplicito per gli eventi di ricerca, calcolando la durata dell’heartbeat in base alla marca temporale del dispositivo, anziché alla posizione della testina di riproduzione.
