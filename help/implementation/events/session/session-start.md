---
title: Avvio sessione
description: Segnala l’inizio di una sessione multimediale e ottieni l’ID sessione richiesto per tutti gli eventi successivi.
feature: Streaming Media
role: Developer
source-git-commit: 6534e4c76dcb4113bbbb99aed2a0e350f9256b15
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 4%

---


# Avvio sessione

L’evento di inizio sessione apre una sessione di tracciamento dei contenuti multimediali. Deve essere il primo evento inviato per qualsiasi riproduzione. La risposta restituisce un ID di sessione che tutti gli eventi successivi per la stessa sessione devono includere.

Una sessione scade automaticamente se **non vengono ricevuti eventi per 10 minuti** o se **non si verifica alcun movimento dell&#39;indicatore di riproduzione per 30 minuti**. Se una sessione scade, devi chiamare di nuovo l’avvio della sessione per ottenere un nuovo ID sessione.

* **Prerequisiti**: nessuno; sempre il primo evento
* **Metrica associata**: [Avvio file multimediale](/help/reporting/metrics/media-starts.md)

## Web SDK

Chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.sessionStart"` e il `sessionDetails` richiesto. La risposta include l&#39;ID sessione in `handle[].payload[].sessionId` (tipo `media-analytics:new-session`). Memorizzare questo valore e passarlo come `sessionID` in tutti gli eventi successivi.

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

Chiamare `trackSessionStart` con un oggetto multimediale e metadati facoltativi.

**iOS (Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Cotlino)**

```kotlin
val mediaObject = Media.createMediaObject("video-123",
                                          "video-id-123",
                                          128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

tracker.trackSessionStart(mediaObject, null)
```

## Roku (BrightScript)

Chiama `createMediaSession` con i dettagli di sessione richiesti:

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

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart). La risposta include l&#39;ID sessione in `handle[].payload[].sessionId` (tipo `media-analytics:new-session`).

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "playerName": "HTML5 Player",
          "contentType": "VOD",
          "length": 128,
          "channel": "Sports"
        },
        "playhead": 0
      }
    }
  }]
}'
```

## Media SDK

Chiamare `trackSessionStart` con un oggetto multimediale creato utilizzando `ADB.Media.createMediaObject`:

```javascript
var mediaObject = ADB.Media.createMediaObject(
  "video-123",                  // name
  "video-id-123",               // media ID
  128,                          // length (seconds)
  ADB.Media.StreamType.VOD,     // stream type
  ADB.Media.MediaType.Video     // media type
);

tracker.trackSessionStart(mediaObject, null);
```

## API Media Collection

Invia un POST `sessionStart` all&#39;endpoint [sessioni](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md). L&#39;intestazione di risposta `Location` contiene l&#39;ID sessione da utilizzare in tutte le richieste di eventi successive.

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports",
    "media.playerName": "HTML5 Player",
    "media.contentType": "vod",
    "media.length": 128,
    "media.id": "video-123"
  }
}
```
