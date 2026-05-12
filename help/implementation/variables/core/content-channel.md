---
title: Canale del contenuto
description: Imposta il canale per identificare la stazione di distribuzione, la rete o la proprietà in cui viene riprodotto il contenuto.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 5%

---


# Canale del contenuto

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Canale contenuto**. Vedi [Canale contenuto](/help/reporting/dimensions/content-channel.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile del canale del contenuto identifica la stazione di distribuzione, la rete o la proprietà in cui viene riprodotto il contenuto. È richiesto per tutte le implementazioni di Streaming Media. Qualsiasi stringa viene accettata. I valori tipici includono un nome di rete, una parte del percorso di un sito o un identificatore di proprietà interno.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.channel` |
| **Campo raccolta XDM** | [`mediaCollection.sessionDetails.channel`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obbligatorio** | Sì |
| **Inviato con** | Avvio della sessione, chiusura della sessione |

## Web SDK

Imposta `channel` all&#39;interno di `mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Impostare il canale tramite la configurazione del tracker durante la creazione del tracker, utilizzando `MediaConstants.TrackerConfig.CHANNEL`. Il canale non fa parte dell’oggetto multimediale.

**iOS (Swift)**

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

**Android (Cotlino)**

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

val tracker = Media.createTracker(config)
```

## Roku (BrightScript)

Imposta `channel` in `mediaCollection.sessionDetails` quando chiama `createMediaSession`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "playhead": 0
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `channel` in `mediaCollection.sessionDetails`:

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
          "channel": "Sports"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Impostare il canale su `ADB.MediaConfig` prima di creare il tracker:

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";

var tracker = ADB.Media.getInstance(mediaConfig);
```

## API Media Collection

Includi `media.channel` nell&#39;oggetto `params` della richiesta POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).
