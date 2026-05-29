---
title: Schema di reporting XDM
description: Scopri quali eventi API di Media Edge generano eventi esperienza in Adobe Experience Platform e come convalidare la tua implementazione utilizzando lo schema XDM mediaReporting.
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3a4d31b-8f9e-4d7a-9b2e-1a5f0e8c7d39
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85eid: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 267532dfbe6dc3f7bcff0991536ae3baf6eff053
workflow-type: tm+mt
source-wordcount: 760
ht-degree: 4%

---


# Schema di reporting XDM

Quando invii eventi di tracciamento dei contenuti multimediali utilizzando Adobe Experience Platform Edge Network, il backend di Media Analytics elabora tali eventi e scrive eventi di esperienza calcolati nei set di dati di Platform. Scopri quali eventi raggiungono Platform e cosa viene calcolato dal backend, per aiutarti a convalidare la tua implementazione e creare rapporti accurati in Customer Journey Analytics o Adobe Analytics.

Due schemi XDM distinti vengono utilizzati in parti diverse della pipeline di raccolta e reporting:

| Schema | Namespace | Direzione | Finalità |
|---|---|---|---|
| Media Collection | `xdm.mediaCollection` | Client → Adobe | Cosa invia il lettore per ogni evento di tracciamento. Utilizzato da [variabili](/help/implementation/variables/). |
| Reporting sui contenuti multimediali | `xdm.mediaReporting` | Piattaforma Adobe → | Cosa scrive il backend nei set di dati dopo l’elaborazione. Utilizzato da [dimensioni](/help/reporting/dimensions/overview.md) e [metriche](/help/reporting/metrics/overview.md). |

I campi presenti in `mediaReporting` ma assenti dal payload `mediaCollection` sono derivati dalla sequenza completa di eventi in una sessione. Non si inviano mai questi campi; Adobe li genera.

## Eventi che scrivono nei set di dati di Platform

Dei 12 tipi di evento tracciabili, solo cinque generano singole scritture di eventi esperienza nei set di dati:

| Tipo di evento | Incluso nei set di dati | Note |
|---|---|---|
| [Inizio sessione](/help/implementation/events/session/session-start.md) | Sì | Scritto quando la sessione viene inizializzata |
| [Inizio annuncio](/help/implementation/events/ads/ad-start.md) | Sì | Scritto quando inizia un singolo annuncio |
| [Annuncio completato](/help/implementation/events/ads/ad-complete.md) | Sì | Scritto quando un annuncio viene riprodotto fino al completamento |
| [Capitolo completato](/help/implementation/events/chapters/chapter-complete.md) | Sì | Scritto quando un capitolo viene riprodotto al completamento |
| [Sessione completata](/help/implementation/events/session/session-complete.md) | Sì | Scritto al termine della sessione; set di campi calcolati più ricco |
| [Riproduci](/help/implementation/events/playback/play.md) | No | Utilizzato per calcolare `timePlayed` |
| [Inizio pausa](/help/implementation/events/playback/pause-start.md) | No | Utilizzato per calcolare `pauseCount` e `pauseTime` |
| [Ping](/help/implementation/events/playback/ping.md) | No | Heartbeat; utilizzato per rilevare l’inattività della sessione |
| [Avvio buffer](/help/implementation/events/playback/buffer-start.md) | No | Utilizzato per calcolare le metriche del buffer QoE |
| [Modifica bitrate](/help/implementation/events/playback/bitrate-change.md) | No | Utilizzato per calcolare le metriche del bitrate QoE |
| [Inizio stato](/help/implementation/events/player-state/state-start.md) | No | Utilizzato per calcolare le metriche dello stato del lettore |
| [Errore](/help/implementation/events/error.md) | No | Utilizzato per calcolare `errorCount` in QoE |

## Campi calcolati dal back-end

I campi seguenti vengono visualizzati nei payload `mediaReporting` ma non fanno mai parte del payload della raccolta. Il backend li deriva dall’intera sequenza di eventi.

**Livello sessione** (visualizzato il `sessionComplete`):

| Campo | Descrizione |
|---|---|
| `xdm.mediaReporting.sessionDetails.timePlayed` | Totale secondi di contenuto principale riprodotto, esclusi gli annunci |
| `xdm.mediaReporting.sessionDetails.totalTimePlayed` | Totale secondi trascorsi, inclusi gli annunci |
| `xdm.mediaReporting.sessionDetails.uniqueTimePlayed` | Secondi deduplicati: gli intervalli visualizzati più di una volta vengono conteggiati una sola volta |
| `xdm.mediaReporting.sessionDetails.averageMinuteAudience` | `timePlayed` diviso per la lunghezza del contenuto |
| `xdm.mediaReporting.sessionDetails.estimatedStreams` | Flussi simultanei stimati |
| `xdm.mediaReporting.sessionDetails.adCount` | Numero di annunci avviati |
| `xdm.mediaReporting.sessionDetails.chapterCount` | Numero di capitoli avviati |
| `xdm.mediaReporting.sessionDetails.pauseCount` / `xdm.mediaReporting.sessionDetails.pauseTime` | Frequenza di pausa e durata totale della pausa |
| `xdm.mediaReporting.sessionDetails.hasProgress10` ... `xdm.mediaReporting.sessionDetails.hasProgress95` | Flag di milestone di avanzamento (10%, 25%, 50%, 75%, 95%) |
| `xdm.mediaReporting.sessionDetails.hasSegmentView` | Indica se è stato visualizzato almeno un fotogramma del contenuto |
| `xdm.mediaReporting.sessionDetails.isCompleted` / `xdm.mediaReporting.sessionDetails.isPlayed` | Flag di completamento e inizio |
| `xdm.mediaReporting.sessionDetails.secondsSinceLastCall` | Tempo trascorso tra l&#39;ultimo ping e la chiusura della sessione |
| `xdm.mediaReporting.sessionDetails.segment` | Parentesi di segmenti di contenuto (ad esempio, `[0-1]`) |

**Livello annuncio** (visualizzato in `adComplete`):

| Campo | Descrizione |
|---|---|
| `xdm.mediaReporting.advertisingDetails.timePlayed` | Secondi di riproduzione del contenuto dell’annuncio |
| `xdm.mediaReporting.advertisingDetails.isCompleted` | Se l’annuncio è stato riprodotto fino al completamento |

**Livello capitolo** (visualizzato in `chapterComplete`):

| Campo | Descrizione |
|---|---|
| `xdm.mediaReporting.chapterDetails.timePlayed` | Secondi di riproduzione del contenuto del capitolo |
| `xdm.mediaReporting.chapterDetails.isCompleted` | Se il capitolo è stato riprodotto fino al completamento |
| `xdm.mediaReporting.chapterDetails.isStarted` | Se il capitolo è stato avviato |

**QoE** (aggregato il `sessionComplete`):

| Campo | Descrizione |
|---|---|
| `xdm.mediaReporting.qoeDataDetails.bitrateAverage` | Bitrate medio nella sessione |
| `xdm.mediaReporting.qoeDataDetails.bitrateAverageBucket` | Intervallo del bitrate medio a periodi fissi |
| `xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` | Numero di modifiche del bitrate |
| `xdm.mediaReporting.qoeDataDetails.errorCount` | Numero di errori |
| `xdm.mediaReporting.qoeDataDetails.droppedFrames` | Totale fotogrammi saltati |
| `xdm.mediaReporting.qoeDataDetails.playerSdkErrors` | Array di codici di errore del lettore |
| `xdm.mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | Se si è verificato un errore |
| `xdm.mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | Se si sono verificati fotogrammi saltati |
| `xdm.mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | Se si sono verificate modifiche del bitrate |

## Contenuto scaricato

Per le sessioni tracciate utilizzando l&#39;endpoint [scaricato](/help/use-cases/track-downloaded-content.md), il backend imposta automaticamente `xdm.mediaReporting.sessionDetails.isDownloaded` su `true` nell&#39;evento di reporting `sessionStart`. Tutti gli altri eventi di reporting per le sessioni scaricate seguono lo stesso schema delle sessioni live. Utilizza questo campo in CJA o Adobe Analytics per filtrare o segmentare la riproduzione scaricata.

Vedi [Endpoint scaricato](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/) nel riferimento API di Media Edge per i dettagli sull&#39;implementazione della raccolta.

## Convalida l’implementazione

Dopo aver inviato gli eventi tramite l’API di Media Edge, verifica che i dati siano arrivati correttamente utilizzando uno dei seguenti metodi:

**Anteprima set di dati Adobe Experience Platform**

1. In [CX Enterprise](https://experience.adobe.com), passa a **[!UICONTROL Datasets]** e seleziona il set di dati di Streaming Media.
2. Seleziona **[!UICONTROL Preview dataset]** per visualizzare gli eventi esperienza acquisiti più di recente.
3. Verificare che `eventType` valori come `media.sessionStart` e `media.sessionComplete` vengano visualizzati con campi `mediaReporting` compilati.

**Ispezione set di dati Customer Journey Analytics**

1. In CJA, apri la connessione associata al set di dati per contenuti multimediali in streaming.
2. Selezionare **Aggiungi set di dati** ed esaminare lo schema per verificare che i campi `mediaReporting` siano mappati alle dimensioni e alle metriche previste.

**Regole di elaborazione di Adobe Analytics (se si utilizza la destinazione Analytics)**

Per le suite di rapporti di Adobe Analytics che ricevono dati tramite il connettore di origine di Analytics, puoi utilizzare le Regole di elaborazione per mappare `mediaReporting` variabili di dati di contesto a proprietà o eVar personalizzate. Il flag `isDownloaded` è disponibile come `a.media.downloaded`.

## Esempi di payload XDM

Gli esempi seguenti mostrano la struttura XDM `mediaReporting` completa per ogni evento di reporting come scritto nei set di dati di Platform. La proprietà `_{tenantName}` rappresenta lo spazio dei nomi tenant della tua organizzazione per qualsiasi campo personalizzato.

+++media.sessionStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "isViewed": true,
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "hasResume": false,
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionStart",
    "_id": "0[...]0",
    "timestamp": "YYYY-11-20T12:43:35Z"
  }
}
```

+++

+++media.adStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "name": "/uri-reference/001",
        "length": 10,
        "siteID": "siteID",
        "isStarted": true,
        "creativeID": "creativeID",
        "friendlyName": "Ad 1"
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adStart",
    "_id": "d[...]0",
    "timestamp": "YYYY-11-20T12:43:56Z"
  }
}
```

+++

+++media.adComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "length": 10,
        "creativeID": "creativeID",
        "timePlayed": 7,
        "name": "/uri-reference/001",
        "siteID": "siteID",
        "friendlyName": "Ad 1",
        "isCompleted": true
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adComplete",
    "_id": "f[...]0",
    "timestamp": "YYYY-11-20T12:44:03Z"
  }
}
```

+++

+++media.chapterComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2",
      "customTest": "myCustomValue1"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "chapterDetails": {
        "timePlayed": 10,
        "offset": 0,
        "length": 10,
        "index": 1,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "isStarted": true,
        "friendlyName": "Chapter 1",
        "isCompleted": true
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.chapterComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:24Z"
  }
}
```

+++

+++media.sessionComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "qoeDataDetails": {
        "playerSdkErrors": ["test-buffer-start"],
        "bitrateAverageBucket": "0-99",
        "bitrateChangeCount": 1,
        "droppedFrames": 30,
        "hasErrorImpactedStreams": true,
        "hasBitrateChangeImpactedStreams": true,
        "hasDroppedFrameImpactedStreams": true,
        "bitrateAverage": 35,
        "timeToStart": 1,
        "errorCount": 1
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "hasProgress10": true,
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "episode": "4933",
        "pauseTime": 3,
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "segment": "[0-1]",
        "season": "1521",
        "showType": "sitcom",
        "pauseCount": 1,
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "uniqueTimePlayed": 47,
        "totalTimePlayed": 55,
        "author": "test-author",
        "hasProgress25": true,
        "feed": "sourceFeed",
        "timePlayed": 48,
        "name": "test-name",
        "publisher": "test-media-publisher",
        "hasPauseImpactedStreams": true,
        "averageMinuteAudience": 0.48,
        "artist": "test-artist",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "hasSegmentView": true,
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "friendlyName": "test-friendly-name",
        "isCompleted": true,
        "playerName": "HTML5 player",
        "album": "test-album",
        "chapterCount": 1,
        "length": 100,
        "adCount": 1,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "secondsSinceLastCall": 51,
        "assetID": "/uri-reference",
        "isPlayed": true,
        "estimatedStreams": 1,
        "firstDigitalDate": "releaseDate"
      },
      "states": [
        {
          "isSet": true,
          "name": "mute",
          "count": 1,
          "time": 3
        },
        {
          "isSet": true,
          "name": "pictureInPicture",
          "count": 1,
          "time": 3
        }
      ]
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:40Z"
  }
}
```

+++

+++media.sessionStart (contenuto scaricato)

Le sessioni tracciate utilizzando l&#39;endpoint [scaricato](/help/use-cases/track-downloaded-content.md) seguono lo stesso schema di reporting con una differenza chiave: `xdm.mediaReporting.sessionDetails.isDownloaded` è impostato su `true` nell&#39;evento di reporting `sessionStart`. Tutti gli altri tipi di evento sono identici agli esempi di contenuto live riportati sopra.

```json
{
  "xdm": {
    "mediaReporting": {
      "customMetadata": [
        {
          "name": "customData",
          "value": "example"
        }
      ],
      "playhead": 0,
      "sessionDetails": {
        "ID": "d8a25708a6b0be83975e32e2f422105ed62f51ff67e6d82d898657534ab9244f",
        "channel": "channel",
        "contentType": "VOD",
        "length": 100,
        "name": "123456789",
        "playerName": "playerName",
        "isDownloaded": true
      }
    },
    "eventType": "media.sessionStart",
    "timestamp": "YYYY-09-26T15:52:24Z",
    "identityMap": {
      "ECID": [
        {
          "id": "51910389753901685456014889838591030721"
        }
      ]
    },
    "implementationDetails": {
      "version": "0.0.1",
      "environment": "browser",
      "name": "https://ns.adobe.com/experience/edge"
    }
  }
}
```

+++
