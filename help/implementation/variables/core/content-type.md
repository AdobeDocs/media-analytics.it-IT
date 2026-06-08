---
title: Tipo di contenuto
description: Imposta il tipo di contenuto per identificare il formato del flusso (VOD, Live, Lineare, podcast, canzone e così via).
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 2%

---


# Tipo di contenuto

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Content type**. Vedi [Tipo di contenuto](/help/reporting/dimensions/content-type.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile del tipo di contenuto identifica il formato del flusso (ad esempio, VOD, Live o Lineare per video o podcast o audiolibro per audio). È richiesta per tutte le implementazioni di Streaming Media e deve essere impostata all’inizio della sessione. I valori definiti da Adobe popolano i segmenti e i rapporti integrati del Tipo di contenuto; anche le stringhe personalizzate sono accettate, ma non corrisponderanno ai segmenti incorporati. Se non viene impostato, il valore predefinito è `missing_content_type`.

Valori consigliati:

* **Video:** `vod`, `live`, `linear`, `ugc`, `dvod`
* **Audio:** `song`, `podcast`, `audiobook`, `radio`

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.contentType` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.sessionDetails.contentType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.contentType` |
| **Obbligatorio** | Sì |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md), chiusura sessione |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `contentType` all&#39;interno di `xdm.mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview):

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

Passa la costante del tipo di contenuto come argomento `streamType` a `createMediaObject`. Utilizzare valori `MediaConstants.StreamType.*` come `VOD`, `LIVE`, `LINEAR`, `AOD`, `PODCAST`. Nota: in Mobile SDK, l&#39;argomento `streamType` controlla il tipo di contenuto. La variabile Stream Type (audio vs. video) è l&#39;argomento separato `mediaType`.

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Passa la costante del tipo di contenuto come argomento `streamType` a `createMediaObject`. Utilizzare valori `MediaConstants.StreamType.*` come `VOD`, `LIVE`, `LINEAR`, `AOD`, `PODCAST`. Nota: in Mobile SDK, l&#39;argomento `streamType` controlla il tipo di contenuto. La variabile Stream Type (audio vs. video) è l&#39;argomento separato `mediaType`.

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Edge Roku]

Imposta `contentType` in `xdm.mediaCollection.sessionDetails` quando chiama `createMediaSession`:

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

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `contentType` in `xdm.mediaCollection.sessionDetails`:

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

Passa una costante `ADB.Media.StreamType.*` come quarto argomento a `ADB.Media.createMediaObject`:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD, // Content type — VOD, LIVE, LINEAR, etc.
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Passa una costante `ADBMobile.media.StreamType.*` come quarto argomento a `ADBMobile.media.createMediaObject`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Passa una costante `MEDIA_STREAM_TYPE_*` come quarto argomento (`streamType`) a `adb_media_init_mediainfo`. In SDK Roku 2.x questo argomento contiene il tipo di contenuto (`vod`, `live`, `linear`):

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API Media Collection]

Includi `media.contentType` nell&#39;oggetto `params` della richiesta POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.contentType": "vod"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).

>[!ENDTABS]
