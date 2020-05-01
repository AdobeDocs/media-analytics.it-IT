---
title: 'Timeline 1: visualizza fino alla fine del contenuto'
description: null
uuid: 0ff591d3-fa99-4123-9e09-c4e71ea1060b
translation-type: tm+mt
source-git-commit: c86c7932f932af0a121e0b757921973d6f4084e8

---


# Timeline 1: visualizza fino alla fine del contenuto{#timeline-view-to-end-of-content}

## VOD, annunci pre-roll, messa in pausa, buffering, visualizzazione del contenuto alla fine

I diagrammi seguenti illustrano la timeline dell&#39;indicatore di riproduzione e la cronologia delle azioni di un utente. I dettagli di ciascuna azione e le relative richieste sono presentati di seguito.


![](assets/va_api_content.png)


![](assets/va_api_actions.png)


## Dettagli azione

### Azione 1 - Avvia sessione {#Action-1}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Riproduzione automatica o Pulsante Riproduci premuto, il video inizia a caricarsi. | 0 | 0 | `/api/v1/sessions` |

**Dettagli implementazione**

Questa chiamata segnala _l&#39;intenzione dell&#39;utente di riprodurre_ un video. <br/><br/>Restituisce un ID sessione ( `{sid}`) al client utilizzato per identificare tutte le chiamate di tracciamento successive all’interno della sessione. Lo stato del lettore non è ancora &quot;play&quot;, ma è invece &quot;start&quot;. <br/><br/>[I parametri di sessione obbligatori ](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) devono essere inclusi nella `params` mappa nel corpo della richiesta. <br/><br/>Sul back-end, questa chiamata genera una chiamata di avvio di Adobe Analytics.

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

### Azione 2 - Avvio timer ping {#Action-2}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app avvia il timer evento | 0 | 0 | `/api/v1/sessions/{sid}/events` |  |

**Dettagli di implementazione**

Avviate il timer di ping dell&#39;app. Il primo evento di ping dovrebbe quindi attivare 1 secondo in se ci sono annunci pre-roll, 10 secondi in caso contrario.

### Azione 3 - Avvio interruzione annuncio {#Action-3}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Avvio pre-roll e interruzione | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Gli annunci possono essere tracciati solo all&#39;interno di un&#39;interruzione di annuncio.

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

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track pre-roll Ad #1 start | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Inizia il tracciamento del primo annuncio pre-roll, che dura 15 secondi. Inclusione di metadati personalizzati con questo `adStart` .

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

### Azione 5 - Punti annuncio {#Action-5}

#### Azione 5.1 - Annuncio ping 1 {#Action-5-1}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia l&#39;evento | 1 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Ping the backend ogni 1 secondo all&#39;interno di un annuncio.

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

#### Azione 5.2 - Annuncio ping 2 {#Action-5-2}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia l&#39;evento | 2 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Ping the backend ogni 1 secondo all&#39;interno di un annuncio.

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

#### Azione 5.3 - Annuncio ping 3 {#Action-5-3}


| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia l&#39;evento | 3 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Ping the backend ogni 1 secondo all&#39;interno di un annuncio.

>[!NOTE]
>
>Gli annunci successivi nella timeline ignorano la serie di ping di un secondo
>nell&#39;interesse della brevità...

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

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track pre-roll Ad #1 completo | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

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

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track pre-roll Ad #2 start | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

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

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia l&#39;evento | 20 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Ping il backend ogni 1 secondo.

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

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track pre-roll Ad #2 completo | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

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

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Traccia pre-roll e interruzione completa | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

La pausa pubblicitaria è finita. Durante la pausa pubblicitaria, lo stato di riproduzione è rimasto &quot;play&quot;.

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

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciare l’evento di riproduzione | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Dopo l’ `adBreakComplete` evento, mettere il lettore nello stato di &quot;riproduzione&quot; utilizzando l’ `play` evento.

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

### Azione 12 - Ping {#Action-12}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia l&#39;evento | 30 | 8 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

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

### Azione 13 - Avvio buffer {#Action-13}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Si è verificato un evento di inizio buffer | 33 | 11 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Tenere traccia dello spostamento del lettore allo stato &quot;buffering&quot;.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    }, eventType:bufferStart
}
```

### Azione 14 - Fine buffer {#Action-14}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Buffering terminato, l&#39;app tiene traccia della ripresa del contenuto | 36 | 11 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Il buffering termina dopo 3 secondi, quindi il lettore torna allo stato di &quot;riproduzione&quot;. È necessario inviare un altro evento di tracciamento che esce dal buffering.  **La`play`chiamata dopo una chiamata`bufferStart`deduce una chiamata &quot;bufferEnd&quot; al back end,** quindi non è necessario un `bufferEnd` evento.

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

### Azione 15 - Ping {#Action-15}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia l&#39;evento | 40 | 15 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Eseguire il ping del backend ogni 10 secondi.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 15,
        ts: <timestamp>
    }, eventType:ping
}
```

### Azione 16 - Inizio interruzione annuncio {#Action-16}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciamento avvio intermedio e interruzione | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Media roll con durata di 8 secondi: send `adBreakStart` .

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

### Azione 17 - Inizio annuncio {#Action-17}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track mid-roll Ad #3 start | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

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

### Azione 18 - Aggiunta di annunci {#Action-18}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia l&#39;evento | 50 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Eseguire il ping del backend ogni 10 secondi.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    }, eventType:ping
}
```

### Azione 19 - Annuncio completo {#Action-19}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Track mid-roll Ad #1 completo | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

L&#39;annuncio mid-roll è completo.

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

### Azione 20 - Fine annuncio {#Action-20}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciamento del mid-roll e interruzione | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

L&#39;interruzione dell&#39;annuncio è completa.

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

### Azione 21 - Ping {#Action-21}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia l&#39;evento | 60 | 27 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

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

### Azione 22 - Pausa {#Action-22}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Pausa utente | 64 | 31 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

L&#39;azione dell&#39;utente sposta lo stato di riproduzione su &quot;Pausa&quot;.

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

### Azione 23 - Ping {#Action-23}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia l&#39;evento | 70 | 31 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Eseguire il ping del backend ogni 10 secondi. Player è ancora nello stato &quot;buffering&quot;; l&#39;utente rimane bloccato a 20 secondi di contenuto. Fuming...

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    }, eventType:ping
}
```

### Azione 24 - Riproduzione {#Action-24}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;utente ha premuto Riproduci per riprendere il contenuto principale | 74 | 31 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Sposta lo stato di riproduzione su &quot;play&quot;.  **La`play`chiamata dopo una chiamata`pauseStart`deduce una chiamata di &quot;ripresa&quot; al back-end,** per cui non è necessario un `resume` evento.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    }, eventType:play
}
```

### Azione 25 - Ping {#Action-25}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia l&#39;evento | 80 | 37 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Eseguire il ping del backend ogni 10 secondi.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 37,
        ts: <timestamp>
    }, eventType:ping
}
```

### Azione 26 - Sessione completata {#Action-26}

| Azione | Timeline azione (secondi) | Posizione dell&#39;indicatore di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;utente ha finito di guardare il contenuto alla fine. | 88 | 45 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Inviate `sessionComplete` al backend per indicare che l&#39;utente ha terminato di guardare l&#39;intero contenuto.

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
>**Nessun evento di ricerca? -** Non esiste alcun supporto esplicito nell&#39;API di Media Collection per `seekStart` eventi o `seekComplete` eventi. Questo perché alcuni lettori generano un numero molto elevato di eventi di questo tipo quando l&#39;utente finale sta scorrendo, e diverse centinaia di utenti potrebbero facilmente strozzare la larghezza di banda di rete di un servizio back-end. Adobe supporta esplicitamente gli eventi di ricerca elaborando la durata del heartbeat in base alla marca temporale del dispositivo, anziché alla posizione dell&#39;indicatore di riproduzione.
