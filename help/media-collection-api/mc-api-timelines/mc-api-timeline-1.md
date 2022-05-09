---
title: Informazioni sulle timeline di tracciamento dei file multimediali Visualizza fino alla fine del contenuto
description: Approfondisci la timeline dell’indicatore di riproduzione e le azioni dell’utente corrispondente. Scopri i dettagli di ciascuna azione e le relative richieste.
uuid: 0ff591d3-fa99-4123-9e09-c4e71ea1060b
exl-id: 16b15e03-5581-471f-ab0c-077189dd32d6
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 88bf699cb5b0872cefa4d6a6609c74f8fa35189a
workflow-type: ht
source-wordcount: '1203'
ht-degree: 100%

---

# Timeline 1 - Visualizza fino alla fine del contenuto {#timeline-view-to-end-of-content}

## VOD, annunci pre-roll, pausa, buffering, visualizzazione del contenuto fino alla fine

I seguenti diagrammi illustrano la timeline della testina di riproduzione e la timeline corrispondente delle azioni di un utente. Di seguito sono riportati i dettagli di ciascuna azione e le relative richieste.


![](assets/va_api_content.png)


![](assets/va_api_actions.png)


## Dettagli azione

### Azione 1 - Avvia sessione {#Action-1}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Premendo il pulsante Riproduzione automatica o Riproduzione, il video inizia a caricarsi. | 0 | 0 | `/api/v1/sessions` |

**Dettagli implementazione**

Questa chiamata segnala _l’intenzione dell’utente di riprodurre_ un video. <br/><br/>Restituisce una sessione ID (`{sid}`) al client utilizzata per identificare tutte le chiamate di tracciamento successive all’interno della sessione. Lo stato del lettore non è ancora “in riproduzione”, ma è “in avvio”. I <br/><br/>[Parametri di sessione obbligatori ](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) devono essere inclusi nella mappa `params` nel corpo della richiesta. <br/><br/>Nel backend, questa chiamata genera una chiamata di avvio Adobe Analytics.

**Esempio di corpo della richiesta**

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

### Azione 2 - Avvio timer del ping {#Action-2}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app avvia il timer dell’evento ping | 0 | 0 | `/api/v1/sessions/{sid}/events` |  |

**Dettagli di implementazione**

Avvia il timer ping dell’app. Il primo evento ping dovrebbe quindi attivarsi in 1 secondo se ci sono annunci pre-roll, 10 secondi in caso contrario.

### Azione 3 - Avvio dell’interruzione pubblicitaria {#Action-3}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento inizio dell’interruzione pubblicitaria pre-roll | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Gli annunci possono essere tracciati solo all’interno di un’interruzione pubblicitaria.

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

### Azione 4 - Avvio dell’annuncio {#Action-4}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento dell’inizio dell’annuncio pre-roll n.1 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Inizia il tracciamento del primo annuncio pre-roll, che è lungo 15 secondi. Inclusione di metadati personalizzati con questo `adStart`.

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

**NOTA: tra gli eventi AdBreakStart e AdStart non devono esserci altri eventi di riproduzione.**

### Azione 5 - Ping annuncio {#Action-5}

#### Azione 5.1 - Ping annuncio 1 {#Action-5-1}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 1 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Effettua il ping del backend ogni 1 secondo all’interno di un annuncio.

**Richiesta di esempio**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

#### Azione 5.2 - Ping annuncio 2 {#Action-5-2}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 2 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Effettua il ping del backend ogni 1 secondo all’interno di un annuncio.

**Richiesta di esempio**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

#### Azione 5.3 - Ping annuncio 3 {#Action-5-3}


| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 3 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Effettua il ping del backend ogni 1 secondo all’interno di un annuncio.

>[!NOTE]
>
>Per gli annunci successivi nella timeline non verrà mostrata la serie di ping di un secondo,
>per brevità...

**Richiesta di esempio**

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

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Traccia il completamento del 1° annuncio pre-roll | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Traccia la fine del primo annuncio pre-roll.

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

### Azione 7 - Avvio dell’annuncio {#Action-7}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Traccia l’inizio del 2° annuncio pre-roll | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Traccia l’inizio del secondo annuncio pre-roll, che ha una durata di 7 secondi.

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

### Azione 8 - Ping dell’annuncio {#Action-8}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 20 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Esegui il ping del backend ogni 1 secondo.

**Richiesta di esempio**

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

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Traccia il completamento del 2° annuncio pre-roll | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Traccia la fine del secondo annuncio pre-roll.

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

### Azione 10 - Completamento dell’interruzione pubblicitaria {#Action-10}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento dell’annuncio pre-roll completato | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

L’interruzione pubblicitaria è terminata. Durante l’interruzione pubblicitaria, lo stato della riproduzione è rimasto “in esecuzione”.

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

### Azione 11 - Riproduci il contenuto {#Action-11}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento dell’evento di riproduzione | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Dopo l’evento `adBreakComplete`, imposta il lettore in stato di “riproduzione” utilizzando l’evento `play`.

**Esempio di corpo della richiesta**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play
}
```

### Azione 12 - Ping {#Action-12}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 30 | 8 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Esegui il ping del backend ogni 10 secondi.

**Esempio di corpo della richiesta**

```
{
    playerTime: {
        playhead: 8,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Azione 13 - Avvio del buffer {#Action-13}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Si è verificato un evento di avvio del buffer | 33 | 11 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Traccia lo spostamento del lettore allo stato di “buffering”.

**Esempio di corpo della richiesta**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    }, eventType:bufferStart
}
```

### Azione 14 - Fine buffer {#Action-14}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Buffering terminato, l’app tiene traccia della ripresa del contenuto | 36 | 11 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Il buffering termina dopo 3 secondi, quindi riporta il lettore allo stato di “riproduzione”. Devi inviare un altro evento di riproduzione del tracciamento proveniente dal buffering. **La chiamata `play` dopo `bufferStart` implica una chiamata “bufferEnd” al back-end,** quindi non è necessario un evento `bufferEnd`.

**Esempio di corpo della richiesta**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:play
}
```

### Azione 15 - Ping {#Action-15}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 40 | 15 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Esegui il ping del backend ogni 10 secondi.

**Esempio di corpo della richiesta**

```
{
    playerTime: {
        playhead: 15,
        ts: <timestamp>
    }, eventType:ping
}
```

### Azione 16 - Avvio dell’interruzione pubblicitaria {#Action-16}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento avvio interruzione pubblicitaria mid-roll | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Annuncio mid-roll con una durata di 8 secondi: invia `adBreakStart`.

**Esempio di corpo della richiesta**

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

### Azione 17 - Inizio annuncio {#Action-17}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento avvio dell’annuncio mid-roll n.3 | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Tracciamento dell’annuncio mid-roll.

**Esempio di corpo della richiesta**

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

### Azione 18 - Ping dell’annuncio {#Action-18}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 50 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Esegui il ping del backend ogni 10 secondi.

**Esempio di corpo della richiesta**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    }, eventType:ping
}
```

### Azione 19 - Annuncio completo {#Action-19}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento annuncio mid-roll n.1 completato | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

L’annuncio mid-roll è completo.

**Esempio di corpo della richiesta**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Azione 20 - Interruzione pubblicitaria completata {#Action-20}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| Tracciamento interruzione pubblicitaria mid-roll completato | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

L’interruzione pubblicitaria è stata completata.

**Esempio di corpo della richiesta**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### Azione 21 - Ping {#Action-21}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 60 | 27 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Esegui il ping del backend ogni 10 secondi.

**Esempio di corpo della richiesta**

```
{
    playerTime: {
        playhead: 27,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Azione 22 - Pausa {#Action-22}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’utente ha premuto pausa | 64 | 31 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

L’azione dell’utente sposta lo stato di riproduzione su “messo in pausa”.

**Esempio di corpo della richiesta**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:pauseStart
}
```

### Azione 23 - Ping {#Action-23}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 70 | 31 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Esegui il ping del backend ogni 10 secondi. Il lettore è ancora in stato di “buffering”; l’utente rimane bloccato a 20 secondi di contenuto. Furente...

**Esempio di corpo della richiesta**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    }, eventType:ping
}
```

### Azione 24 - Play {#Action-24}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’utente ha premuto Play per riprendere il contenuto principale | 74 | 31 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Sposta lo stato di riproduzione su “in riproduzione”.  **La chiamata `play` dopo `pauseStart` deduce una chiamata di “ripresa” al back end,** quindi non è necessario un evento `resume`.

**Esempio di corpo della richiesta**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    }, eventType:play
}
```

### Azione 25 - Ping {#Action-25}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’app invia un evento ping | 80 | 37 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Esegui il ping del backend ogni 10 secondi.

**Esempio di corpo della richiesta**

```
{
    playerTime: {
        playhead: 37,
        ts: <timestamp>
    }, eventType:ping
}
```

### Azione 26 - Sessione completa {#Action-26}

| Azione | Timeline di azioni (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta del client |
| --- | :---: | :---: | --- |
| L’utente termina di guardare il contenuto fino alla fine. | 88 | 45 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Invia `sessionComplete` al backend per indicare che l’utente ha terminato di guardare l’intero contenuto.

**Corpo di esempio della richiesta**

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
>**Nessun evento di ricerca? -** Non è disponibile alcun supporto esplicito nell’API di Media Collection per eventi `seekStart` o `seekComplete`. Alcuni utenti generano un numero molto elevato di tali eventi nel momento in cui l’utente finale esegue la pulizia. Inoltre, è probabile che le diverse centinaia di utenti causino un bottleneck della larghezza di banda di un servizio back-end. Adobe si basa su un supporto esplicito per gli eventi di ricerca, calcolando la durata dell’heartbeat in base alla marca temporale del dispositivo, anziché alla posizione della testina di riproduzione.
