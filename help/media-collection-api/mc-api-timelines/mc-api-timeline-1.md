---
seo-title: Timeline 1 - Visualizza alla fine del contenuto
title: Timeline 1 - Visualizza alla fine del contenuto
uuid: 0 ff 591 d 3-fa 99-4123-9 e 09-c 4 e 71 ea 1060 b
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Timeline 1 - View to end of content{#timeline-view-to-end-of-content}

## VOD, annunci pre-roll, pausa, buffering, visualizzazione del contenuto alla fine

I diagrammi seguenti illustrano la timeline della linea di scansione e la cronologia corretta delle azioni di un utente. I dettagli per ogni azione e le relative richieste sono presentati di seguito.


![](assets/va_api_content.png)


![](assets/va_api_actions.png)


## Dettagli azione

### Action 1 - Start session {#Action-1}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| È stato attivato il pulsante Riproduzione automatica o Riproduci, il video inizia a caricarsi. | 0 | 0 | `/api/v1/sessions` |

**Dettagli implementazione**

This call signals _the user's intention to play_ a video. <br/><br/>Restituisce un ID sessione ( `{sid}`) al client utilizzato per identificare tutte le chiamate di tracciamento successive all'interno della sessione. Lo stato del lettore non è ancora "playing", ma viene invece "starting". <br/><br/>[I parametri di sessione obbligatori ](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) devono essere inclusi nella `params` mappa nel corpo della richiesta. <br/><br/>Sul retro, questa chiamata genera una chiamata ad Adobe Analytics.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 0, ts: <timestamp>
    },
    eventType:sessionStart, params: {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR_TS_ ]",
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

### Action 2 - Ping timer start {#Action-2}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app avvia il timer dell'evento ping | 0 | 0 | `/api/v1/sessions/{sid}/events` |  |

**Dettagli di implementazione**

Avviate il timer di ping dell'app. Il primo evento di ping dovrebbe quindi attivarsi 1 secondo in presenza di annunci pre-roll, 10 secondi in caso contrario.

### Action 3 - Ad break start {#Action-3}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tenere traccia dell'avvio di annunci di annunci prerroll | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Gli annunci possono essere tracciati solo all'interno di un'interruzione di annuncio.

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

### Action 4 - Ad start {#Action-4}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track pre-roll Ad # 1 start | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Inizia a tracciare il primo annuncio precedente, che dura 15 secondi. Including custom metadata with this `adStart` .

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 0,
        ts: &lt;timestamp&gt;
    },
    eventType:adStart,
    params: {
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
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement"
    },
    customMetadata: {
        "myCustomData1": "CustomData1",
        "myCustomData2": "CustomData2"
    }
}
```

### Action 5 - Ad pings {#Action-5}

#### Action 5.1 - Ad ping 1 {#Action-5-1}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento ping | 1 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Ping il backend ogni 1 secondi all'interno di un annuncio.

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

#### Action 5.2 - Ad ping 2 {#Action-5-2}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento ping | 2 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Ping il backend ogni 1 secondi all'interno di un annuncio.

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

#### Action 5.3 - Ad ping 3 {#Action-5-3}


| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento ping | 3 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Ping il backend ogni 1 secondi all'interno di un annuncio.

>[!NOTE]
>
>Gli annunci successivi nella timeline ignoreranno la visualizzazione della serie di un secondo
>a scopo di brevità…

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

### Action 6 - Ad complete {#Action-6}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track pre-roll Ad # 1 complete | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Tieni traccia della fine del primo annuncio precedente.

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

### Action 7 - Ad start {#Action-7}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track pre-roll Ad # 2 start | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Tieni traccia dell'inizio del secondo annuncio precedente, che dura 7 secondi.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
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
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Action 8 - Ad pings {#Action-8}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento ping | 20 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Ping il backend ogni 1 secondi.

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

### Action 9 - Ad complete {#Action-9}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track pre-roll Ad # 2 complete | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Tieni traccia della fine del secondo annuncio precedente.

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

### Action 10 - Ad break complete {#Action-10}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciamento dell'interruzione di annunci pre-roll | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

L'interruzione di annunci è finita. Durante l'interruzione di annunci, lo stato di riproduzione è rimasto «playing».

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

### Action 11 - Play content {#Action-11}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Evento di riproduzione della traccia | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

After the `adBreakComplete` event, put the player is in the "playing" state using the `play` event.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play
}
```

### Action 12 - Ping {#Action-12}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento ping | 30 | 8 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Ping il backend ogni 10 secondi.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 8,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 13 - Buffer start {#Action-13}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Evento Avvio buffer si è verificato | 33 | 11 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Consente di tenere traccia dello spostamento del lettore allo stato «buffering».

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    }, eventType:bufferStart
}
```

### Action 14 - Buffer end {#Action-14}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Il buffering termina, l'app tiene traccia della ripresa del contenuto | 36 | 11 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Il buffering termina dopo 3 secondi, quindi riposizionate il lettore sullo stato «playing». Dovete inviare un altro evento di riproduzione della traccia che non proviene dal buffering. **La`play`chiamata dopo una`bufferStart`chiamata a "bufferend" viene chiamata al back end,** quindi non è necessario un `bufferEnd` evento.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:play
}
```

### Action 15 - Ping {#Action-15}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento ping | 40 | 15 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Ping il backend ogni 10 secondi.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 15,
        ts: <timestamp>
    }, eventType:ping
}
```

### Action 16 - Ad break start {#Action-16}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tenere traccia dell'avvio delle interruzioni di annunci mid-roll | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Mid-roll ad of 8 seconds duration: send `adBreakStart` .

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakStart,
    params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 21
    }
}
```

### Action 17 - Ad start {#Action-17}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track mid-roll Ad # 3 start | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Tieni traccia dell'annuncio mid.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adStart, params: {
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
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Action 18 - Ad ping {#Action-18}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento ping | 50 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Ping il backend ogni 10 secondi.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    }, eventType:ping
}
```

### Action 19 - Ad complete {#Action-19}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track mid-roll Ad # 1 complete | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

L'annuncio mid-roll è completo.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Action 20 - Ad break complete {#Action-20}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciamento dell'interruzione di annunci mid-roll | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

L'interruzione di annuncio è completa.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### Action 21 - Ping {#Action-21}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento ping | 60 | 27 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Ping il backend ogni 10 secondi.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 27,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 22 - Pause {#Action-22}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'utente preme Pausa | 64 | 31 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

L'azione dell'utente sposta lo stato di riproduzione in "pausa".

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:pauseStart
}
```

### Action 23 - Ping {#Action-23}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento ping | 70 | 31 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Ping il backend ogni 10 secondi. Player è ancora nello stato «buffering»; l'utente si blocca a 20 secondi di contenuto. Fumatura…

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    }, eventType:ping
}
```

### Action 24 - Play {#Action-24}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'utente è stato premuto per riprendere il contenuto principale | 74 | 31 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Sposta lo stato di riproduzione in «riproduzione». **La`play`chiamata dopo una`pauseStart`sezione deduce una chiamata "resume" alla fine,** quindi non è necessario un `resume` evento.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    }, eventType:play
}
```

### Action 25 - Ping {#Action-25}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento ping | 80 | 37 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Ping il backend ogni 10 secondi.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 37,
        ts: <timestamp>
    }, eventType:ping
}
```

### Action 26 - Session complete {#Action-26}

| Azione | Timeline azione (secondi) | Posizione Playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'utente ha terminato di guardare il contenuto alla fine. | 88 | 45 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Send `sessionComplete` to the backend to indicate that the user finished watching the entire content.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 45,
        ts: <timestamp>
    }, eventType:sessionComplete
}
```

>[!NOTE]
>
>**No Seek Events? -** There is no explicit support in the Media Collection API for `seekStart` or `seekComplete` events. poiché alcuni lettori generano un numero molto elevato di tali eventi quando l'utente finale scorre, e centinaia di utenti potrebbero facilmente rallentare la larghezza di banda di rete di un servizio di back-end. Adobe aggirava il supporto esplicito per gli eventi di ricerca calcolando la durata heartbeat basata sulla marca temporale del dispositivo, piuttosto che sulla posizione della testina.

