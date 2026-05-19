---
title: Episodio
description: Impostare il numero di episodio per il contenuto episodico in modo che i singoli episodi possano essere riportati separatamente.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 7%

---


# Episodio

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Episodio**. Vedi [Episodio](/help/reporting/dimensions/episode.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile dell&#39;episodio è il numero dell&#39;episodio all&#39;interno della stagione (in genere un numero intero di stringa come `"13"`). Accoppia con [Show](/help/implementation/variables/standard-metadata/show.md) e [Season](/help/implementation/variables/standard-metadata/season.md) in modo che il coinvolgimento possa essere suddiviso per singolo episodio.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.episode` |
| **Campo raccolta XDM** | [`mediaCollection.sessionDetails.episode`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.episode` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md), chiusura sessione |

## Web SDK

Imposta `episode` all&#39;interno di `mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        episode: "13"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Passa il numero dell&#39;episodio come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.EPISODE`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.EPISODE] = "13"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Cotlino)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.EPISODE] = "13"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilizza `createMediaSession` per impostare `episode` in `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "episode": "13"
            },
            "playhead": 0
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `episode` in `mediaCollection.sessionDetails`:

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
          "episode": "13"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Passa l&#39;episodio nell&#39;oggetto `contextData` utilizzando `ADB.Media.VideoMetadataKeys.Episode`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Episode] = "13";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Includi `media.episode` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.episode": "13"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).
