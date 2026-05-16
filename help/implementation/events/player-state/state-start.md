---
title: Avvio stato
description: Segnala che il lettore multimediale è entrato in uno stato del lettore tracciato.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 5%

---


# Avvio stato

L’evento di avvio dello stato segnala che il lettore multimediale è entrato in uno stato tracciato come schermo intero, disattivazione audio o sottotitoli. Un lettore può essere in più stati contemporaneamente e gli stati possono essere avviati e terminati nella stessa chiamata evento. Chiudi ogni stato con un evento [Fine stato](state-end.md).

Nomi di stato validi: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture`, `inFocus`

* **Prerequisiti**: [Inizio sessione](../session/session-start.md)
* **Metrica associata**: varia in base allo stato. Vedere [Tracciamento dello stato del lettore](/help/use-cases/player-state-tracking/implementation-and-reporting.md)

## Web SDK

Chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.statesUpdate"` e il nome dello stato in `statesStart`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

È possibile avviare più stati nella stessa chiamata:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [
        { name: "fullscreen" },
        { name: "mute" }
      ],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

## Mobile SDK

Utilizzare `trackPlayerStateStart` con un oggetto stato creato dalla costante `MediaConstants.PlayerState` appropriata.

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateStart, info: stateObject, metadata: nil)
```

**Android (Cotlino)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateStart, stateObject, null)
```

## Roku (BrightScript)

Chiamare `sendMediaEvent` con `eventType: "media.statesUpdate"` e il nome dello stato in `statesStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "fullscreen" }],
            "playhead": 60
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) con il nome dello stato in `statesStart`:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 60,
        "statesStart": [{ "name": "fullscreen" }]
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

tracker.trackPlayerStateStart(stateObject);
```

## API Media Collection

Invia un POST `stateStart` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```
