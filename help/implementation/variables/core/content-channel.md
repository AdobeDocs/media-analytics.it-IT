---
title: Canale del contenuto
description: Imposta il canale per identificare la stazione di distribuzione, la rete o la proprietà in cui viene riprodotto il contenuto.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 2%
---

# Canale del contenuto

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Canale contenuto**. Vedi [Canale contenuto](/help/reporting/dimensions/content-channel.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile del canale del contenuto identifica la stazione di distribuzione, la rete o la proprietà in cui viene riprodotto il contenuto. È richiesto per tutte le implementazioni di Streaming Media. Qualsiasi stringa viene accettata. I valori tipici includono un nome di rete, una parte del percorso di un sito o un identificatore di proprietà interno.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.channel` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.sessionDetails.channel`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.channel` |
| **Obbligatorio** | Sì |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md), chiusura sessione |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `channel` all&#39;interno di `xdm.mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview):

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

>[!TAB iOS]

Impostare il canale tramite la configurazione del tracker durante la creazione del tracker, utilizzando `MediaConstants.TrackerConfig.CHANNEL`. Il canale non fa parte dell’oggetto multimediale.

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

>[!TAB Android]

Impostare il canale tramite la configurazione del tracker durante la creazione del tracker, utilizzando `MediaConstants.TrackerConfig.CHANNEL`. Il canale non fa parte dell’oggetto multimediale.

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

val tracker = Media.createTracker(config)
```

>[!TAB Edge Roku]

Imposta `channel` in `xdm.mediaCollection.sessionDetails` quando chiama `createMediaSession`:

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

>[!TAB API Media Edge]

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `channel` in `xdm.mediaCollection.sessionDetails`:

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

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Impostare il canale su `ADB.MediaConfig` prima di creare il tracker:

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";

var tracker = ADB.Media.getInstance(mediaConfig);
```

>[!TAB Chromecast]

Passa `channel` come chiave metadati standard quando chiami `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var metadata = { "a.media.channel": "Sports" };
ADBMobile.media.trackSessionStart(mediaInfo, metadata);
```

>[!TAB Roku 2.x]

Imposta `channel` nella sezione `mediaHeartbeat` di `ADBMobileConfig.json`. Il canale è un valore di configurazione, non un valore per sessione:

```json
"mediaHeartbeat": {
  "channel": "Sports"
}
```

>[!TAB API Media Collection]

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

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/sessions).

>[!ENDTABS]
