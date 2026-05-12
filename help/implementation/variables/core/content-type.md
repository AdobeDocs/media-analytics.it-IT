---
title: Tipo di contenuto
description: Imposta il tipo di contenuto per identificare il formato del flusso (VOD, Live, Lineare, podcast, canzone e così via).
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 4%

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
| **Campo raccolta XDM** | [`mediaCollection.sessionDetails.contentType`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obbligatorio** | Sì |
| **Inviato con** | Avvio della sessione, chiusura della sessione |

## Web SDK

Imposta `contentType` all&#39;interno di `mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

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

Passa la costante del tipo di contenuto come argomento `streamType` a `createMediaObject`. Utilizzare valori `MediaConstants.StreamType.*` come `VOD`, `LIVE`, `LINEAR`, `AOD`, `PODCAST`. Nota: in Mobile SDK, l&#39;argomento `streamType` controlla il tipo di contenuto. La variabile Stream Type (audio vs. video) è l&#39;argomento separato `mediaType`.

**iOS (Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Cotlino)**

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

## Roku (BrightScript)

Imposta `contentType` in `mediaCollection.sessionDetails` quando chiama `createMediaSession`:

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

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `contentType` in `mediaCollection.sessionDetails`:

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

## API Media Collection

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
