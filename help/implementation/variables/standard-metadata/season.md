---
title: Stagione
description: Imposta il numero di stagione per i contenuti episodici in modo che il coinvolgimento possa essere suddiviso per stagione.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 7%

---


# Stagione

>[!BEGINSHADEBOX]

*Questa pagina riguarda la raccolta dati per la variabile **Season**. Vedi [Stagione](/help/reporting/dimensions/season.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile della stagione è il numero della stagione per lo spettacolo (in genere un numero intero di stringa come `"2"`). Impostalo per i contenuti che fanno parte di una serie in modo che il coinvolgimento possa essere suddiviso per stagione. Accoppia con [Show](/help/implementation/variables/standard-metadata/show.md) e [Episode](/help/implementation/variables/standard-metadata/episode.md) per il contesto episodico completo.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.season` |
| **Campo raccolta XDM** | [`mediaCollection.sessionDetails.season`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obbligatorio** | No |
| **Inviato con** | Avvio della sessione, chiusura della sessione |

## Web SDK

Imposta `season` all&#39;interno di `mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        season: "2"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Passa la stagione come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.SEASON`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.SEASON] = "2"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Cotlino)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.SEASON] = "2"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilizza `createMediaSession` per impostare `season` in `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "season": "2"
            },
            "playhead": 0
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `season` in `mediaCollection.sessionDetails`:

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
          "season": "2"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Passa la stagione nell&#39;oggetto `contextData` utilizzando `ADB.Media.VideoMetadataKeys.Season`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Season] = "2";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Includi `media.season` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.season": "2"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).
