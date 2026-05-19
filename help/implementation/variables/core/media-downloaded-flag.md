---
title: Flag di contenuto multimediale scaricato
description: Contrassegna una sessione come riproduzione offline scaricata in modo che venga segnalata separatamente dalle sessioni in streaming.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 4%

---


# Flag di contenuto multimediale scaricato

>[!BEGINSHADEBOX]

*In questa pagina è illustrata la raccolta dati per la variabile **Flag di contenuto multimediale scaricato**. Vedi [File multimediali scaricati](/help/reporting/dimensions/media-downloaded-flag.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

Il flag Media Download indica che una sessione sta riproducendo contenuto offline scaricato in precedenza anziché un flusso live da Internet. Impostarlo durante l&#39;inizializzazione del tracker (Mobile SDK) o includerlo nel payload `sessionStart` (Edge/Media Collection API). Usa questo flag per separare la riproduzione offline dalle sessioni in streaming nel reporting.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.downloaded` |
| **Campo raccolta XDM** | [`mediaCollection.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.downloaded` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md), chiusura sessione |

## Web SDK

Imposta `isDownloaded` su `true` all&#39;interno di `mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

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
        streamType: "video",
        isDownloaded: true
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Impostare il flag di contenuto scaricato sulla configurazione del tracker durante la creazione del tracker, utilizzando `MediaConstants.TrackerConfig.DOWNLOADED_CONTENT`.

**iOS (Swift)**

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

**Android (Cotlino)**

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

val tracker = Media.createTracker(config)
```

## Roku (BrightScript)

Imposta `isDownloaded` su `true` all&#39;interno di `mediaCollection.sessionDetails` durante la chiamata a `createMediaSession`:

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
                "streamType": "video",
                "isDownloaded": true
            },
            "playhead": 0
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [downloaded](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/#downloaded) dopo che il dispositivo è tornato online, eseguendo il batch dell&#39;intera sessione offline in `mediaDownloadedEvents`. Adobe imposta automaticamente `isDownloaded` su `true` e assegna un ID sessione; non includere nessuno dei due nel payload.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.downloaded",
      "mediaDownloadedEvents": [
        {
          "mediaEventTimestamp": "YYYY-09-26T15:52:24+00:00",
          "mediaEventType": "media.sessionStart",
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
        },
        {
          "mediaEventTimestamp": "YYYY-09-26T15:54:32+00:00",
          "mediaEventType": "media.sessionComplete",
          "mediaCollection": {
            "playhead": 128
          }
        }
      ]
    }
  }]
}
```

## Media SDK

Imposta `downloadedContent` su `ADB.MediaConfig` prima di creare il tracker:

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";
mediaConfig.downloadedContent = true;

var tracker = ADB.Media.getInstance(mediaConfig);
```

## API Media Collection

Includi `media.downloaded` nell&#39;oggetto `params` della richiesta POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.downloaded": true
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).
