---
title: Nome del lettore di contenuti
description: Imposta il nome del lettore per identificare quale lettore ha eseguito il rendering del contenuto.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 2%

---


# Nome del lettore di contenuti

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Content player name**. Vedi [Nome lettore di contenuti](/help/reporting/dimensions/content-player-name.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile del nome del lettore di contenuto identifica quale lettore ha eseguito il rendering del contenuto (ad esempio, `HTML5 Player`, `Brightcove` o `Roku Player`). È richiesta per tutte le implementazioni di Streaming Media e deve essere impostata all’inizio della sessione. Il valore viene utilizzato nella dimensione Nome lettore di contenuti per confrontare il coinvolgimento e la qualità tra i lettori nella stessa proprietà.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.playerName` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.sessionDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.playerName` |
| **Obbligatorio** | Sì |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md), chiusura sessione |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `playerName` all&#39;interno di `xdm.mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview):

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

Impostare il nome del lettore tramite la configurazione del tracker durante la creazione del tracker, utilizzando `MediaConstants.TrackerConfig.PLAYER_NAME`. Il nome del lettore non fa parte dell’oggetto multimediale.

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

>[!TAB Android]

Impostare il nome del lettore tramite la configurazione del tracker durante la creazione del tracker, utilizzando `MediaConstants.TrackerConfig.PLAYER_NAME`. Il nome del lettore non fa parte dell’oggetto multimediale.

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

val tracker = Media.createTracker(config)
```

>[!TAB Roku]

Imposta `playerName` in `xdm.mediaCollection.sessionDetails` quando chiama `createMediaSession`:

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

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `playerName` in `xdm.mediaCollection.sessionDetails`:

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

Imposta il nome del lettore su `ADB.MediaConfig` prima di creare il tracciatore:

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";

var tracker = ADB.Media.getInstance(mediaConfig);
```

>[!TAB Chromecast]

Passa il nome del lettore come chiave di metadati standard quando chiami `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var metadata = { "a.media.playerName": "Chromecast Player" };
ADBMobile.media.trackSessionStart(mediaInfo, metadata);
```

>[!TAB API Media Collection]

Includi `media.playerName` nell&#39;oggetto `params` della richiesta POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.playerName": "HTML5 Player"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).

>[!ENDTABS]
