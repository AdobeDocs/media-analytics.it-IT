---
title: Tipo di feed multimediale
description: Identifica il tipo di feed (ad esempio, East-HD o West-SD) per contenuti che variano in base all’area geografica o alla qualità.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 6%

---


# Tipo di feed multimediale

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Tipo di feed multimediale**. Vedi [Tipo di feed multimediale](/help/reporting/dimensions/media-feed-type.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile del tipo di feed multimediale identifica il feed di trasmissione (ad esempio, `"East-HD"`, `"West-SD"` o `"4K"`). Utilizzalo quando lo stesso contenuto viene distribuito tramite più feed regionali o di qualità e il coinvolgimento deve essere suddiviso per feed.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.feed` |
| **Campo raccolta XDM** | [`mediaCollection.sessionDetails.feed`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obbligatorio** | No |
| **Inviato con** | Avvio della sessione, chiusura della sessione |

## Web SDK

Imposta `feed` all&#39;interno di `mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        feed: "East-HD"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Passa il tipo di feed come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.MEDIA_FEED`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.MEDIA_FEED] = "East-HD"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Cotlino)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.MEDIA_FEED] = "East-HD"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilizza `createMediaSession` per impostare `feed` in `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "feed": "East-HD"
            },
            "playhead": 0
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `feed` in `mediaCollection.sessionDetails`:

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
          "feed": "East-HD"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Passa il feed nell&#39;oggetto `contextData` utilizzando `ADB.Media.VideoMetadataKeys.Feed`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Feed] = "East-HD";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Includi `media.feed` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.feed": "East-HD"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).
