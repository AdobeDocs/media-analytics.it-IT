---
title: Fine stato
description: Segnala che il lettore multimediale è uscito da uno stato del lettore tracciato.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 5%

---


# Fine stato

L’evento di fine stato segnala che il lettore multimediale è uscito da uno stato tracciato come schermo intero, disattivazione audio o sottotitoli. Invia per chiudere uno stato aperto da [Inizio stato](state-start.md). Gli stati possono essere avviati e terminati nella stessa chiamata evento. Un lettore può uscire simultaneamente da più stati.

Nomi di stato validi: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture`, `inFocus`

* **Prerequisiti**: [Inizio sessione](../session/session-start.md), [Inizio stato](state-start.md)
* **Metrica associata**: varia in base allo stato. Vedere [Tracciamento dello stato del lettore](/help/use-cases/player-state-tracking/implementation-and-reporting.md)

## Web SDK

Chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.statesUpdate"` e il nome dello stato in `statesEnd`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

Gli stati possono essere avviati e terminati nella stessa chiamata:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }],
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

Utilizzare `trackPlayerStateEnd` con un oggetto stato creato dalla costante `MediaConstants.PlayerState` appropriata.

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateEnd, info: stateObject, metadata: nil)
```

**Android (Cotlino)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateEnd, stateObject, null)
```

## Roku (BrightScript)

Chiamare `sendMediaEvent` con `eventType: "media.statesUpdate"` e il nome dello stato in `statesEnd`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "fullscreen" }],
            "playhead": 90
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) con il nome dello stato in `statesEnd`:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 90,
        "statesEnd": [{ "name": "fullscreen" }]
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

Utilizza `ADB.Media.createStateObject` con la costante `ADB.Media.PlayerState` appropriata:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Fullscreen);

tracker.trackPlayerStateEnd(stateObject);
```

## API Media Collection

Invia un POST `stateEnd` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```
