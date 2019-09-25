---
seo-title: Timeline 3 - Capitoli
title: Timeline 3 - Capitoli
uuid: 41b52072-e1cd-4dda-9253-31f3408924f6
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Timeline 3 - Capitoli {#timeline-3-chapters}

## VOD, annunci pre-roll, messa in pausa, buffering, visualizzazione del contenuto alla fine


I diagrammi seguenti illustrano la timeline dell'indicatore di riproduzione e la cronologia corrispondente delle azioni di un utente. I dettagli di ciascuna azione e le relative richieste sono presentati di seguito.


![](assets/va_api_content_3.png)


![](assets/va_api_actions_3.png)


## Dettagli azione


### Azione 1 - Avvia sessione {#Action-1}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Riproduzione automatica o Pulsante Riproduci premuto, il video inizia a caricarsi. | 0 | 0 | `/api/v1/sessions` |

**Dettagli di implementazione**

Questa chiamata segnala _l’intenzione dell’utente di riprodurre_ un video. Restituisce un ID sessione ( `{sid}` ) al client utilizzato per identificare tutte le chiamate di tracciamento successive all’interno della sessione. Lo stato del lettore non è ancora "play", ma è "start".  [I parametri](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) di sessione obbligatori devono essere inclusi nella `params` mappa nel corpo della richiesta.  Sul back-end, questa chiamata genera una chiamata di avvio di Adobe Analytics.

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

### Azione 2 - Avvio del timer di ping {#Action-2}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app avvia il timer evento | 0 | 0 |  |

**Dettagli di implementazione**

Avviate il timer di ping. Il primo evento di ping dovrebbe quindi attivare 1 secondo in se ci sono annunci pre-roll, 10 secondi in caso contrario.

### Azione 3 - Avvio interruzione annuncio {#Action-3}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Avvio pre-roll e interruzione | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

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
        "media.ad.podIndex": 0, "media.ad.podSecond": 0
    }
}
```

### Azione 4 - Inizio annuncio {#Action-4}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track pre-roll Ad #1 start | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Inizia il tracciamento del primo annuncio pre-roll, che dura 15 secondi. Inserimento di metadati personalizzati con questo `adStart` .

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

### Azione 5 - Punti annuncio {#Action-5}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento | 10 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Ping il backend ogni 1 secondo. (Gli annunci successivi non vengono visualizzati nell'interesse della brevità.)

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
| Track pre-roll Ad #1 completo | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Tieni traccia della fine del primo annuncio pre-roll.

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

### Azione 7 - Inizio annuncio {#Action-7}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track pre-roll Ad #2 start | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Tieni traccia dell’inizio del secondo annuncio pre-roll, che dura 7 secondi.

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

### Azione 8 - Punti annuncio {#Action-8}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento | 16 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Ping il backend ogni 1 secondo. (Gli annunci successivi non vengono visualizzati nell'interesse della brevità.)

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

### Azione 9 - Annuncio completato {#Action-9}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track pre-roll Ad #2 completo | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Tieni traccia della fine del secondo annuncio pre-roll.

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

### Azione 10 - Fine annuncio {#Action-10}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Traccia pre-roll e interruzione | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

La pausa pubblicitaria è finita. Durante la pausa pubblicitaria, lo stato di riproduzione è rimasto "play".

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

### Azione 11 - Riproduci contenuto {#Action-11}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciare l’evento di riproduzione | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Dopo l’ `adBreakComplete` evento, mettere il lettore nello stato di "riproduzione" utilizzando l’ `play` evento.

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

### Azione 12 - Inizio capitolo {#Action-12}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Evento inizio capitolo traccia | 23 | 1 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Dopo l'evento play, tieni traccia dell'inizio del primo capitolo.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:chapterStart, params: {
        "media.chapter.index": 1,
        "media.chapter.offset": 0, "media.chapter.length": 20, "media.chapter.friendlyName": "Chapter Uno"
    },
}
```

### Azione 13 - Ping {#Action-13}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento | 30 | 8 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Eseguire il ping del backend ogni 10 secondi.

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

### Azione 14 - Inizio buffer {#Action-14}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Si è verificato un evento di inizio buffer | 33 | 11 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Tenere traccia dello spostamento nello stato "buffering".

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:bufferStart
}
```

### Azione 15 - Fine buffer (play) {#Action-15}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Buffering terminato, l'app tiene traccia della ripresa del contenuto | 36 | 11 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Il buffering termina dopo 3 secondi, quindi il lettore torna allo stato di "riproduzione". È necessario inviare un altro evento di tracciamento che esce dal buffering.  **La`play`chiamata dopo una chiamata`bufferStart`deduce una chiamata "bufferEnd" al back end,** quindi non è necessario un `bufferEnd` evento.

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

### Azione 16 - Ping {#Action-16}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento | 40 | 15 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Eseguire il ping del backend ogni 10 secondi.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 15,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Azione 17 - Capo finale {#Action-17}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Fine capitolo delle tracce dell'app | 45 | 20 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Il primo capitolo termina, subito prima del secondo annuncio.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 20,
        ts: <timestamp>
    },
    eventType:chapterEnd
}
```

### Azione 18 - Inizio interruzione annuncio {#Action-18}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciamento avvio intermedio e interruzione | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Media roll con durata di 8 secondi: send `adBreakStart` .

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1, "media.ad.podSecond": 21
    }
}
```

### Azione 19 - Inizio annuncio {#Action-19}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track mid-roll Ad #3 start | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Tieni traccia dell’annuncio mid-roll.

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

### Azione 20 - Annunci {#Action-20}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento | 47 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Ping il backend ogni 1 secondo. (Gli annunci successivi non vengono visualizzati nell'interesse della brevità.)

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Azione 21 - Annuncio completato {#Action-21}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track mid-roll Ad #1 completo | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

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

### Azione 22 - Fine annuncio {#Action-22}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Traccia metà rullo e interruzione completa | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

L'interruzione dell'annuncio è completa.

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

### Azione 23 - Inizio capitolo {#Action-23}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciare l'inizio del capitolo 2 | 55 | 22 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**



**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 22,
        ts: <timestamp>
    },
    eventType:chapterStart, params: {
        "media.chapter.index": 2,
        "media.chapter.offset": 22, "media.chapter.length": 22, "media.chapter.friendlyName": "Chapter Dos"
    },
}
```

### Azione 24 - Ping {#Action-24}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento | 60 | 27 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Eseguire il ping del backend ogni 10 secondi.

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

### Azione 25 - Pausa {#Action-25}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Pausa utente | 64 | 31 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

L’azione dell’utente sposta lo stato di riproduzione su "Pausa".

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

### Azione 26 - Ping {#Action-26}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento | 70 | 31 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Eseguire il ping del backend ogni 10 secondi. Player è ancora nello stato "buffering"; l'utente rimane bloccato a 20 secondi di contenuto. Fuming...

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Azione 27 - Riproduci contenuto {#Action-27}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'utente ha premuto Riproduci per riprendere il contenuto principale | 74 | 31 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Sposta lo stato di riproduzione su "play".  **La`play`chiamata dopo una chiamata`pauseStart`deduce una chiamata di "ripresa" al back-end**, per cui non è necessario un `resume` evento.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:play
}
```

### Azione 28 - Ping {#Action-28}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'app invia un evento | 80 | 37 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Eseguire il ping del backend ogni 10 secondi.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 37,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Azione 29 - Capo finale {#Action-29}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Capitolo 2 | 87 | 44 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Traccia la fine del secondo e ultimo capitolo.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:chapterEnd
}
```

### Azione 30 - Sessione completata {#Action-30}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L'utente ha finito di guardare il contenuto alla fine. | 88 | 45 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Inviate `sessionComplete` al backend per indicare che l'utente ha terminato di guardare l'intero contenuto.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 45,
        ts: <timestamp>
    },
    eventType:sessionComplete
}
```


>[!NOTE]
>
>**Nessun evento di ricerca? -** Non esiste alcun supporto esplicito nell'API di Media Collection per `seekStart` eventi o `seekComplete` eventi. Questo perché alcuni lettori generano un numero molto elevato di eventi di questo tipo quando l'utente finale sta scorrendo, e diverse centinaia di utenti potrebbero facilmente strozzare la larghezza di banda di rete di un servizio back-end. Adobe supporta esplicitamente gli eventi di ricerca elaborando la durata del heartbeat in base alla marca temporale del dispositivo, anziché alla posizione dell'indicatore di riproduzione.

