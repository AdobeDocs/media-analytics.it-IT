---
title: Genere
description: Imposta il genere di contenuto come stringa delimitata da virgole. Il contenuto multi-genere si suddivide tra gli elementi di riga nel reporting.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 6%

---


# Genere

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Genre**. Vedi [Genere](/help/reporting/dimensions/genre.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile di genere è il genere di contenuto definito dal produttore (ad esempio, `"Drama"`, `"Comedy"` o `"Drama,Action"`). Delimita con virgole più valori quando il contenuto è adatto a più di un genere. Nella generazione rapporti, la variabile elenco suddivide ogni valore in una riga separata, con ogni riga che riceve lo stesso peso metrico.

>[!NOTE]
>
>Nella pipeline di reporting, il valore del genere è esposto come `mediaReporting.sessionDetails.genreList` (un campo elenco). Il percorso `mediaReporting.sessionDetails.genre` precedente rimane funzionante, ma si consiglia `genreList`.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.genre` |
| **Campo raccolta XDM** | [`mediaCollection.sessionDetails.genre`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.genre` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md), chiusura sessione |

## Web SDK

Imposta `genre` all&#39;interno di `mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        genre: "Drama,Action"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Passa la stringa del genere come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.GENRE`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Cotlino)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilizza `createMediaSession` per impostare `genre` in `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "genre": "Drama,Action"
            },
            "playhead": 0
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `genre` in `mediaCollection.sessionDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "genre": "Drama,Action"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Passa il genere nell&#39;oggetto `contextData` utilizzando `ADB.Media.VideoMetadataKeys.Genre`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Genre] = "Drama,Action";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Includi `media.genre` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.genre": "Drama,Action"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).
