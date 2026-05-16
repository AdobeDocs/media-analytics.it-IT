---
title: Tipo di flusso
description: Imposta il tipo di flusso per identificare se un flusso multimediale è un contenuto audio o video.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 5%

---


# Tipo di flusso

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Stream type**. Vedi [Tipo di flusso](/help/reporting/dimensions/stream-type.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile del tipo di flusso identifica se un flusso multimediale è un contenuto audio o video. È richiesto per tutte le implementazioni di contenuti multimediali in streaming e deve essere impostato all’inizio di ogni sessione multimediale.

L’impostazione corretta del tipo di flusso è fondamentale per i rapporti multimediali in streaming. Abilita i segmenti predefiniti di **Tipo di flusso multimediale** in Adobe Analytics (solo per contenuti multimediali, solo audio e solo video) e gestisce il reporting audio e video separato in Customer Journey Analytics. Inoltre, assicura che i dati della sessione siano classificati correttamente in tutta la pipeline di analisi dei contenuti multimediali. Le sessioni con un tipo di flusso non impostato o non valido possono essere raggruppate o classificate in modo errato nei rapporti a valle.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.streamType` |
| **Campo raccolta XDM** | [`mediaCollection.sessionDetails.streamType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.streamType` |
| **Obbligatorio** | Sì |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md), chiusura sessione |

## Web SDK

Imposta `streamType` all&#39;interno di `mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "My Video",
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

Passa `Media.MediaType.Video` o `Media.MediaType.Audio` come argomento `mediaType` a `createMediaObject`. Si noti che l&#39;argomento `streamType` in `createMediaObject` controlla la variabile del tipo di contenuto (VOD, Live, ecc.), non questa variabile.

**iOS (Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                                id: "video-id",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Cotlino)**

```kotlin
var mediaInfo = Media.createMediaObject("video-123",
                                        "video-id",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

## Roku (BrightScript)

Imposta `streamType` in `mediaCollection.sessionDetails` quando chiama `createMediaSession`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "My Video",
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

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `streamType` in `mediaCollection.sessionDetails`:

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
          "streamType": "video"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Passa `ADB.Media.MediaType.Video` o `ADB.Media.MediaType.Audio` come quinto argomento a `Media.createMediaObject`:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",               // name
  "video-123",              // media ID
  128,                      // length (seconds)
  ADB.Media.StreamType.VOD, // content type
  ADB.Media.MediaType.Video // stream type: Video or Audio
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Includi `media.streamType` nell&#39;oggetto `params` della richiesta POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.streamType": "video"
  }
}
```

Per la struttura completa delle richieste e per tutti i campi obbligatori, consulta il [riferimento alle sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).
