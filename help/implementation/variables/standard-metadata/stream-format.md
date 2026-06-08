---
title: Formato flusso
description: Imposta il formato del flusso per identificare il livello di qualità (HD, SD o un’altra etichetta utilizzata dalla pipeline di consegna).
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 4%

---


# Formato flusso

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Formato flusso**. Vedere [Formato flusso](/help/reporting/dimensions/stream-format.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile del formato del flusso identifica il livello di qualità del flusso (in genere `"HD"` o `"SD"`, ma qualsiasi stringa viene accettata). Impostalo quando desideri interrompere il coinvolgimento, il completamento o la qualità per livello di qualità della consegna.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.format` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.sessionDetails.streamFormat`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.format` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md), chiusura sessione |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `streamFormat` all&#39;interno di `xdm.mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        streamFormat: "HD"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passa il formato del flusso come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.STREAM_FORMAT`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.STREAM_FORMAT] = "HD"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Passa il formato del flusso come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.STREAM_FORMAT`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.STREAM_FORMAT] = "HD"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Edge Roku]

Utilizza `createMediaSession` per impostare `streamFormat` in `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "streamFormat": "HD"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `streamFormat` in `xdm.mediaCollection.sessionDetails`:

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
          "streamFormat": "HD"
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

Passa il formato del flusso nell&#39;oggetto `contextData` utilizzando `ADB.Media.VideoMetadataKeys.StreamFormat`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.StreamFormat] = "HD";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Utilizzare `ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT` per impostare il formato del flusso nella proprietà `StandardMediaMetadata` dell&#39;oggetto multimediale prima di chiamare `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT] = "HD";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Utilizzare `MEDIA_VideoMetadataKeySTREAM_FORMAT` per impostare il formato del flusso nei metadati standard dell&#39;oggetto multimediale prima di chiamare `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeySTREAM_FORMAT] = "HD"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API Media Collection]

Includi `media.streamFormat` nell&#39;oggetto `params` della richiesta POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.streamFormat": "HD"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).

>[!ENDTABS]
