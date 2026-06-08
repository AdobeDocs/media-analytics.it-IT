---
title: Tipo di spettacolo
description: Identifica il formato del contenuto (episodio completo, anteprima, clip o altro) utilizzando un codice intero stringa.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 4%

---


# Tipo di spettacolo

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Show type**. Vedi [Mostra tipo](/help/reporting/dimensions/show-type.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile show type identifica il formato del contenuto utilizzando un codice intero stringa:

* `"0"`: episodio completo
* `"1"`: anteprima o trailer
* `"2"`: Clip
* `"3"`: Altro

Utilizzatela per separare la visualizzazione di un programma completo da contenuti brevi come trailer e clip durante la misurazione del coinvolgimento.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.type` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.sessionDetails.showType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.type` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md), chiusura sessione |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `showType` all&#39;interno di `xdm.mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        showType: "0"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passa il tipo di visualizzazione come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.SHOW_TYPE`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.SHOW_TYPE] = "0"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Passa il tipo di visualizzazione come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.SHOW_TYPE`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.SHOW_TYPE] = "0"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Edge Roku]

Utilizza `createMediaSession` per impostare `showType` in `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "showType": "0"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `showType` in `xdm.mediaCollection.sessionDetails`:

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
          "showType": "0"
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

Passa il tipo di presentazione nell&#39;oggetto `contextData` utilizzando `ADB.Media.VideoMetadataKeys.ShowType`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.ShowType] = "0";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Utilizzare `ADBMobile.media.VideoMetadataKeys.SHOW_TYPE` per impostare il tipo di presentazione nella proprietà `StandardMediaMetadata` dell&#39;oggetto multimediale prima di chiamare `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.SHOW_TYPE] = "0";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Utilizzare `MEDIA_VideoMetadataKeySHOW_TYPE` per impostare il tipo di presentazione nei metadati standard dell&#39;oggetto multimediale prima di chiamare `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeySHOW_TYPE] = "0"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API Media Collection]

Includi `media.showType` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.showType": "0"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).

>[!ENDTABS]
