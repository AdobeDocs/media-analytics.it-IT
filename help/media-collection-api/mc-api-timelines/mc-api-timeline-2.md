---
title: Timeline 2 - Sessione di abbandono utenti
description: null
uuid: 74b89e8f-ef56-4e0c-b9a8-40739e15b4cf
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Timeline 2 - Sessione di abbandono utenti {#timeline--2-user-abandons-session}

## VOD, annunci pre-roll, annunci mid-roll, l'utente abbandona il contenuto in anticipo

I diagrammi seguenti illustrano la timeline dell'indicatore di riproduzione e la cronologia corrispondente delle azioni di un utente. I dettagli di ciascuna azione e le relative richieste sono presentati di seguito.


![](assets/va_api_content_2.png)


![](assets/va_api_actions_2.png)


## Dettagli azione

### Azione 1 - Avvia sessione {#Action-1}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Pulsante Riproduzione automatica o Riproduzione premuto | 0 | 0 | `/api/v1/sessions` |

**Dettagli implementazione**

Questa chiamata segnala _l'intenzione dell'utente di riprodurre_ un video. Restituisce un ID sessione ( `{sid}` ) al client utilizzato per identificare tutte le chiamate di tracciamento successive all’interno della sessione. Lo stato del lettore non è ancora "play", ma è "start".  [I parametri](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) di sessione obbligatori devono essere inclusi nella `params` mappa nel corpo della richiesta.  Sul back-end, questa chiamata genera una chiamata di avvio di Adobe Analytics.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:sessionStart, params: {
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

### Azione 2 - Avvio timer ping {#Action-2}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app avvia il timer evento | 0 | 0 |  |

**Dettagli implementazione**

Avviate il timer di ping dell'app. Il primo evento di ping dovrebbe quindi attivare 1 secondo in se ci sono annunci pre-roll, 10 secondi in caso contrario.

### Azione 3 - Avvio interruzione annuncio {#Action-3}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Avvio pre-roll e interruzione | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Gli annunci pre-roll devono essere tracciati. Gli annunci possono essere tracciati solo all'interno di un'interruzione di annuncio.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0,
        "media.ad.podSecond": 0
    }
}
```

### Azione 4 - Inizio annuncio {#Action-4}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track pre-roll Ad #1 start | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Viene avviato un annuncio di 12 secondi.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
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

### Azione 5 - Punti annuncio {#Action-5}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento | 1 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Ping il backend ogni 1 secondo. (Gli annunci successivi non sono mostrati, nell'interesse della brevità.)

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Azione 6 - Annuncio completato {#Action-6}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track pre-roll Ad #1 completo | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Il primo annuncio pre-roll è terminato.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Azione 7: interruzione annuncio completata {#Action-7}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Traccia pre-roll e interruzione | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

La pausa pubblicitaria è finita. Durante la pausa pubblicitaria, il giocatore è rimasto nello stato "play".

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### Azione 8 - Riproduci contenuto {#Action-8}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciare l’evento di riproduzione | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Spostare il lettore allo stato "play"; iniziare il tracciamento dell’inizio della riproduzione del contenuto.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play,
    qoeData: { bitrate: 10000 }
}
```

### Azione 9 - Ping {#Action-9}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento | 20 | 8 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Eseguire il ping del backend ogni 10 secondi.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 8ß,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Azione 10 - Ping {#Action-10}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento | 30 | 18 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Eseguire il ping del backend ogni 10 secondi.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 18,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Azione 11 - Errore {#Action-11}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Errore. L'app invia informazioni sull'errore. | 32 | 20 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**


**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 20,
        ts: <timestamp>
    },
    eventType:error
}
```

### Azione 12 - Riproduci contenuto {#Action-12}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app viene recuperata dall'errore, l'utente preme Play | 37 | 20 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**



**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 18,
        ts: <timestamp>
    },
    eventType:play, qoeData: { bitrate: 10000 }
}
```

### Azione 13 - Ping {#Action-13}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento | 40 | 28 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Eseguire il ping del backend ogni 10 secondi.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 28,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Azione 14 - Inizio interruzione annuncio {#Action-14}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciamento avvio intermedio e interruzione | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Media roll con durata di 8 secondi: send `adBreakStart` .

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 33,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 33
    }
}
```

### Azione 15 - Inizio annuncio {#Action-15}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track mid-roll Ad #1 start | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Tieni traccia dell’annuncio mid-roll.

**Corpo della richiesta di esempio**

```
{
    playerTime: { playhead: 33, ts: <timestamp>
    },
    eventType:adStart, params: {
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
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Azione 16 - Chiudi app {#Action-16}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'utente chiude l'app. L'app determina che l'utente ha abbandonato la visualizzazione e non torna a questa sessione. | 48 | 33 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Inviare `sessionEnd` al back-end VA per indicare che la sessione deve essere chiusa immediatamente, senza ulteriore elaborazione.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 33,
        ts: <timestamp>
    },
    eventType:sessionEnd
}
```


