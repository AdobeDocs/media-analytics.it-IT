---
title: Avvio stato
description: Segnala che il lettore multimediale è entrato in uno stato del lettore tracciato.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 2%

---


# Avvio stato

L’evento di avvio dello stato segnala che il lettore multimediale è entrato in uno stato tracciato come schermo intero, disattivazione audio o sottotitoli. Un lettore può essere in più stati contemporaneamente e gli stati possono essere avviati e terminati nella stessa chiamata evento. Chiudi ogni stato con un evento [Fine stato](state-end.md).

Nomi di stato validi: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture`, `inFocus`

* **Prerequisiti**: [Inizio sessione](../session/session-start.md)
* **Metrica associata**: varia in base allo stato; vedi [Tracciare gli stati del lettore](/help/implementation/events/player-state/overview.md)

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.statesUpdate"` e il nome dello stato in `statesStart`:

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

>[!TAB iOS]

Utilizzare `trackPlayerStateStart` con un oggetto stato creato dalla costante `MediaConstants.PlayerState` appropriata.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateStart, info: stateObject, metadata: nil)
```

>[!TAB Android]

Utilizzare `trackPlayerStateStart` con un oggetto stato creato dalla costante `MediaConstants.PlayerState` appropriata.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateStart, stateObject, null)
```

>[!TAB Roku]

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

>[!TAB API Media Edge]

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

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Utilizza `ADB.Media.createStateObject` con la costante `ADB.Media.PlayerState` appropriata:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Fullscreen);

tracker.trackPlayerStateStart(stateObject);
```

>[!TAB Chromecast]

Utilizza `ADBMobile.media.createStateObject` con la costante `ADBMobile.media.PlayerState` appropriata:

```javascript
var stateObject = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);

ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
```

>[!TAB API Media Collection]

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

>[!ENDTABS]
