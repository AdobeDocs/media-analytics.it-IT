---
title: Informazioni sulle timeline di tracciamento dei file multimediali � sessione di abbandono degli utenti
description: Scopri la timeline dell’indicatore di riproduzione e l’azione � dall’utente quando una sessione video viene abbandonata. Scopri i dettagli di ogni azione e richiesta.
uuid: 74b89e8f-ef56-4e0c-b9a8-40739e15b4cf
exl-id: 0c6a89f4-7949-4623-8ed9-ce1d1547bdfa
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 8%

---

# Timeline 2: utente abbandona la sessione {#timeline--2-user-abandons-session}

## VOD, annuncio pre-roll, annunci mid-roll, l&#39;utente abbandona i contenuti in anticipo

I seguenti diagrammi illustrano la timeline della testina di riproduzione e la corrispondente timeline delle azioni di un utente. Di seguito sono riportati i dettagli di ciascuna azione e le relative richieste.


![](assets/va_api_content_2.png)


![](assets/va_api_actions_2.png)


## Dettagli azione

### Azione 1 - Avvia sessione {#Action-1}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Pulsante Riproduzione automatica o Riproduzione premuto | 0 | 0 | `/api/v1/sessions` |

**Dettagli di implementazione**

Questa chiamata segnala _l&#39;intenzione dell&#39;utente di riprodurre_ un video. Restituisce un ID sessione ( `{sid}` ) al client utilizzato per identificare tutte le chiamate di tracciamento successive all’interno della sessione. Lo stato del giocatore non è ancora &quot;in riproduzione&quot;, ma è invece &quot;in partenza&quot;.  [I ](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) parametri di sessione obbligatori devono essere inclusi nella  `params` mappa nel corpo della richiesta.  Nel backend, questa chiamata genera una chiamata di avvio Adobe Analytics.

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
| L&#39;app avvia il timer dell&#39;evento | 0 | 0 |  |

**Dettagli di implementazione**

Avvia il timer ping dell&#39;app. Il primo evento ping dovrebbe quindi attivarsi di 1 secondo in se ci sono annunci pre-roll, 10 secondi in caso contrario.

### Azione 3 - Avvio dell&#39;interruzione dell&#39;annuncio {#Action-3}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Traccia inizio pre-roll annuncio | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Gli annunci pre-roll devono essere tracciati. Gli annunci possono essere tracciati solo all’interno di un’interruzione pubblicitaria.

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

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Traccia l&#39;inizio dell&#39;annuncio pre-roll n. 1 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Inizia un annuncio di 12 secondi.

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

### Azione 5: ping di annunci {#Action-5}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia un evento ping | 1 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Eseguire il ping del backend ogni 1 secondo. (Gli annunci successivi non vengono visualizzati, nell’interesse della brevità.)

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

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciamento annuncio pre-roll n. 1 completato | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Il primo annuncio pre-roll è finito.

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
| Tracciamento pre-roll annuncio completato | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

La pausa pubblicitaria è finita. Durante la pausa pubblicitaria, il giocatore è rimasto in stato di &quot;riproduzione&quot;.

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

### Azione 8 - Riprodurre il contenuto {#Action-8}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciare un evento di riproduzione | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Spostare il lettore allo stato di &quot;riproduzione&quot;; inizia a tenere traccia dell’inizio della riproduzione del contenuto.

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
| L&#39;app invia un evento ping | 20 | 8 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Esegui il ping del backend ogni 10 secondi.

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
| L&#39;app invia un evento ping | 30 | 18 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Esegui il ping del backend ogni 10 secondi.

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
| Errore. L&#39;app invia informazioni sull&#39;errore. | 32 | 20 | `/api/v1/sessions/{sid}/events` |

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

### Azione 12 - Riprodurre il contenuto {#Action-12}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app si riprende dall&#39;errore, l&#39;utente preme Play | 37 | 20 | `/api/v1/sessions/{sid}/events` |

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

### Azione 13 - Ping {#Action-13}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| L&#39;app invia un evento ping | 40 | 28 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Esegui il ping del backend ogni 10 secondi.

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

### Azione 14 - Inizio dell’interruzione dell’annuncio {#Action-14}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Tracciamento inizio interruzione annuncio mid-roll | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Media roll con una durata di 8 secondi: invia `adBreakStart` .

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

### Azione 15 - Inizio dell&#39;annuncio {#Action-15}

| Azione | Timeline azione (secondi) | Posizione testina di riproduzione (secondi) | Richiesta client |
| --- | :---: | :---: | --- |
| Inizio tracciamento annuncio mid-roll n. 1 | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

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
| L’utente chiude l’app. L’app determina che l’utente ha abbandonato la visualizzazione e non ritorna a questa sessione. | 48 | 33 | `/api/v1/sessions/{sid}/events` |

**Dettagli di implementazione**

Inviare `sessionEnd` al backend VA per indicare che la sessione deve essere chiusa immediatamente, senza ulteriore elaborazione.

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
