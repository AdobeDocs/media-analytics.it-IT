---
seo-title: Timeline 2 - Sessione utenti abbandonati
title: Timeline 2 - Sessione utenti abbandonati
uuid: 74 b 89 e 8 f-ef 56-4 e 0 c-b 9 a 8-40739 e 15 b 4 cf
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Timeline 2 - User abandons session {#timeline--2-user-abandons-session}

## VOD, annunci pre-roll, annunci intermedi, utenti abbandonati in anticipo

I diagrammi seguenti illustrano la timeline della linea di scansione e la timeline corrispondente delle azioni di un utente. I dettagli per ogni azione e le relative richieste sono presentati di seguito.


![](assets/va_api_content_2.png)


![](assets/va_api_actions_2.png)


## Dettagli azione

### Action 1 - Start session {#Action-1}

| Azione | Timeline azione (secondi) | Posizione playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Riproduzione automatica o pulsante Riproduci | 0 | 0 | `/api/v1/sessions` |

**Dettagli di implementazione**

This call signals _the user's intention to play_ a video. It returns a Session ID ( `{sid}` ) to the client that is used to identify all subsequent tracking calls within the session. Lo stato del lettore non è ancora "playing", ma viene invece "starting". [I parametri di sessione obbligatori](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) devono essere inclusi nella `params` mappa nel corpo della richiesta. Sul retro, questa chiamata genera una chiamata ad Adobe Analytics.

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

### Action 2 - Ping timer start {#Action-2}

| Azione | Timeline azione (secondi) | Posizione playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app avvia il timer dell'evento ping | 0 | 0 |  |

**Dettagli di implementazione**

Avviate il timer di ping dell'app. Il primo evento di ping dovrebbe quindi attivarsi 1 secondo in presenza di annunci pre-roll, 10 secondi in caso contrario.

### Action 3 - Ad break start {#Action-3}

| Azione | Timeline azione (secondi) | Posizione playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tenere traccia dell'avvio di annunci di annunci prerroll | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

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

### Action 4 - Ad start {#Action-4}

| Azione | Timeline azione (secondi) | Posizione playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track pre-roll Ad # 1 start | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Viene avviato un secondo di 12 secondi.

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

### Action 5 - Ad pings {#Action-5}

| Azione | Timeline azione (secondi) | Posizione playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento ping | 1 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Ping il backend ogni 1 secondi. (Gli annunci successivi non vengono visualizzati, a scopo di brevità.)

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

| Azione | Timeline azione (secondi) | Posizione playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track pre-roll Ad # 1 complete | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Il primo annuncio precedente è finito.

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

### Action 7 - Ad break complete {#Action-7}

| Azione | Timeline azione (secondi) | Posizione playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciamento dell'interruzione di annunci pre-roll | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

L'interruzione di annunci è finita. Durante l'interruzione di annunci, il lettore è rimasto nello stato «playing».

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

### Action 8 - Play content {#Action-8}

| Azione | Timeline azione (secondi) | Posizione playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Evento di riproduzione della traccia | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Spostare il lettore sullo stato «playing»; inizia a tracciare l'inizio della riproduzione del contenuto.

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

### Action 9 - Ping {#Action-9}

| Azione | Timeline azione (secondi) | Posizione playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento ping | 20 | 8 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Ping il backend ogni 10 secondi.

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

### Action 10 - Ping {#Action-10}

| Azione | Timeline azione (secondi) | Posizione playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento ping | 30 | 18 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Ping il backend ogni 10 secondi.

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

### Action 11 - Error {#Action-11}

| Azione | Timeline azione (secondi) | Posizione playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Si verifica un errore, l'app invia informazioni sugli errori. | 32 | 20 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**


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

### Action 12 - Play content {#Action-12}

| Azione | Timeline azione (secondi) | Posizione playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Ripristino dell'app da un errore, l'utente preme Play | 37 | 20 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**



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

### Action 13 - Ping {#Action-13}

| Azione | Timeline azione (secondi) | Posizione playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento ping | 40 | 28 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Ping il backend ogni 10 secondi.

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

### Action 14 - Ad break start {#Action-14}

| Azione | Timeline azione (secondi) | Posizione playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tenere traccia dell'avvio delle interruzioni di annunci mid-roll | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Mid-roll ad of 8 seconds duration: send `adBreakStart` .

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

### Action 15 - Ad start {#Action-15}

| Azione | Timeline azione (secondi) | Posizione playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track mid-roll Ad # 1 start | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Tieni traccia dell'annuncio mid.

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

### Action 16 - Close app {#Action-16}

| Azione | Timeline azione (secondi) | Posizione playhead (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'utente chiude l'app. L'app determina che l'utente ha abbandonato la visualizzazione e non sta tornando a questa sessione. | 48 | 33 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Send `sessionEnd` to the VA backend to indicate that the session should be closed immediately, with no further processing.

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


