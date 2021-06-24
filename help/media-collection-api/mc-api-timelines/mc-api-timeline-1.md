---
title: Informazioni sulle timeline di tracciamento dei file multimediali � Visualizza fino alla fine del contenuto
description: Approfondisci la timeline dell’indicatore di riproduzione e le azioni � dall’utente corrispondente. Scopri i dettagli di ciascuna azione e le relative richieste.
uuid: 0ff591d3-fa99-4123-9e09-c4e71ea1060b
exl-id: 16b15e03-5581-471f-ab0c-077189dd32d6
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 7%

---

# Timeline 1: visualizza fino alla fine del contenuto{#timeline-view-to-end-of-content}

## VOD, annunci pre-roll, messa in pausa, buffering, visualizzazione del contenuto alla fine

I seguenti diagrammi illustrano la timeline della testina di riproduzione e la sequenza temporale corrispondente delle azioni di un utente. Di seguito sono riportati i dettagli di ciascuna azione e le relative richieste.


![](assets/va_api_content.png)


![](assets/va_api_actions.png)


## Dettagli azione

### Azione 1 - Avvia sessione {#Action-1}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Pulsante Riproduzione automatica o Riproduzione premuto, il video inizia a caricarsi. | 0 | 0 | `/api/v1/sessions` |

**Dettagli implementazione**

Questa chiamata segnala _l&#39;intenzione dell&#39;utente di riprodurre_ un video. <br/><br/>Restituisce un ID sessione (  `{sid}`) al client utilizzato per identificare tutte le chiamate di tracciamento successive all’interno della sessione. Lo stato del giocatore non è ancora &quot;in riproduzione&quot;, ma è invece &quot;in partenza&quot;. <br/><br/>[I parametri di sessione obbligatori  ](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) devono essere inclusi nella  `params` mappa nel corpo della richiesta. <br/><br/>Nel backend, questa chiamata genera una chiamata di avvio Adobe Analytics.

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

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app avvia il timer dell&#39;evento | 0 | 0 | `/api/v1/sessions/{sid}/events` |  |

**Dettagli di implementazione**

Avvia il timer ping dell&#39;app. Il primo evento ping dovrebbe quindi attivarsi di 1 secondo in se ci sono annunci pre-roll, 10 secondi in caso contrario.

### Azione 3 - Avvio dell&#39;interruzione dell&#39;annuncio {#Action-3}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Traccia inizio pre-roll annuncio | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

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

### Azione 4 - Avvio dell&#39;annuncio {#Action-4}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Traccia l&#39;inizio dell&#39;annuncio pre-roll n. 1 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Inizia a tenere traccia del primo annuncio pre-roll, che è lungo 15 secondi. Inclusione di metadati personalizzati con questo `adStart` .

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

### Azione 5: ping di annunci {#Action-5}

#### Azione 5.1 - Annunci ping 1 {#Action-5-1}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia un evento ping | 1 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Effettua il ping del backend ogni 1 secondo all’interno di un annuncio.

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

#### Azione 5.2 - Annunci ping 2 {#Action-5-2}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia un evento ping | 2 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Effettua il ping del backend ogni 1 secondo all’interno di un annuncio.

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

#### Azione 5.3 - Annunci ping 3 {#Action-5-3}


| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia un evento ping | 3 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Effettua il ping del backend ogni 1 secondo all’interno di un annuncio.

>[!NOTE]
>
>Gli annunci successivi nella timeline ignorano la visualizzazione della serie di ping di un secondo
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

### Azione 6 - Annuncio completo {#Action-6}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciamento annuncio pre-roll n. 1 completato | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Monitora la fine del primo annuncio pre-roll.

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

### Azione 7 - Avvio dell&#39;annuncio {#Action-7}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Traccia l&#39;inizio dell&#39;annuncio pre-roll n. 2 | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Tieni traccia dell’inizio del secondo annuncio pre-roll, che è lungo 7 secondi.

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

### Azione 8 - Elementi ad ping {#Action-8}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia un evento ping | 20 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Eseguire il ping del backend ogni 1 secondo.

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

### Azione 9 - Annuncio completo {#Action-9}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciamento annuncio pre-roll n. 2 completo | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Monitora la fine del secondo annuncio pre-roll.

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

### Azione 10 - Completamento dell’interruzione dell’annuncio {#Action-10}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciamento pre-roll annuncio completato | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

La pausa pubblicitaria è finita. Durante la pausa pubblicitaria, lo stato di gioco è rimasto &quot;play&quot;.

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

### Azione 11 - Riprodurre il contenuto {#Action-11}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciare un evento di riproduzione | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Dopo l&#39;evento `adBreakComplete`, lo stato &quot;play&quot; del lettore viene inserito utilizzando l&#39;evento `play` .

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

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia un evento ping | 30 | 8 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Esegui il ping del backend ogni 10 secondi.

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

### Azione 13 - Avvio del buffer {#Action-13}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Si è verificato un evento di avvio del buffer | 33 | 11 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Monitora lo spostamento del lettore allo stato di &quot;buffering&quot;.

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

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Buffering terminato, l’app tiene traccia della ripresa del contenuto | 36 | 11 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Il buffering termina dopo 3 secondi, quindi riportare il lettore allo stato di &quot;riproduzione&quot;. Devi inviare un altro evento di riproduzione del brano che esce dal buffering.  **La  `play` chiamata dopo una chiamata  `bufferStart` deduce una chiamata &quot;bufferEnd&quot; al back-end,** quindi non è necessario un  `bufferEnd` evento.

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

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia un evento ping | 40 | 15 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Esegui il ping del backend ogni 10 secondi.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 15,
        ts: <timestamp>
    }, eventType:ping
}
```

### Azione 16 - Avvio ad break {#Action-16}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciamento inizio interruzione annuncio mid-roll | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Media roll con una durata di 8 secondi: invia `adBreakStart` .

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

### Azione 17 - Inizio dell’annuncio {#Action-17}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Traccia avvio annuncio mid-roll n. 3 | 46 | 21 | `/api/v1/sessions/{sid}/events` |

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

### Azione 18 - ping di annunci {#Action-18}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia un evento ping | 50 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Esegui il ping del backend ogni 10 secondi.

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

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciamento annuncio mid-roll n. 1 completato | 54 | 21 | `/api/v1/sessions/{sid}/events` |

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

### Azione 20 - Annuncio interrotto completato {#Action-20}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciamento interruzione annuncio mid-roll completato | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

L&#39;interruzione pubblicitaria è completa.

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

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia un evento ping | 60 | 27 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Esegui il ping del backend ogni 10 secondi.

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

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Pausa utente premuto | 64 | 31 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

L&#39;azione dell&#39;utente sposta lo stato di riproduzione su &quot;messo in pausa&quot;.

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

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia un evento ping | 70 | 31 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Esegui il ping del backend ogni 10 secondi. Il lettore è ancora nello stato &quot;buffering&quot;; l’utente rimane bloccato a 20 secondi di contenuto. Fumare...

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    }, eventType:ping
}
```

### Azione 24 - Gioco {#Action-24}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;utente ha premuto Play per riprendere il contenuto principale | 74 | 31 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Sposta lo stato di riproduzione su &quot;riproduzione&quot;.  **La  `play` chiamata dopo una chiamata  `pauseStart` deduce una chiamata di &quot;ripresa&quot; al back-end,** quindi non è necessario un  `resume` evento.

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

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia un evento ping | 80 | 37 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Esegui il ping del backend ogni 10 secondi.

**Corpo della richiesta di esempio**

```
{
    playerTime: {
        playhead: 37,
        ts: <timestamp>
    }, eventType:ping
}
```

### Azione 26 - Sessione completa {#Action-26}

| Azione | Timeline azione (secondi) | Posizione della testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L’utente termina di guardare il contenuto alla fine. | 88 | 45 | `/api/v1/sessions/{sid}/events` |

**Dettagli implementazione**

Invia `sessionComplete` al backend per indicare che l&#39;utente ha terminato di guardare l&#39;intero contenuto.

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
>**Niente Eventi di ricerca? -** Non è disponibile alcun supporto esplicito nell’API Media Collection per gli eventi `seekStart` o `seekComplete`. Questo perché alcuni giocatori generano un numero molto elevato di tali eventi quando l&#39;utente finale sta pulendo, e diverse centinaia di utenti potrebbero facilmente strozzare la larghezza di banda di rete di un servizio back-end. L&#39;Adobe si basa su un supporto esplicito per gli eventi di ricerca, calcolando la durata dell&#39;heartbeat in base alla marca temporale del dispositivo, anziché alla posizione dell&#39;indicatore di riproduzione.
