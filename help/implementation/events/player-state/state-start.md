---
title: Avvio stato
description: Segnala che il lettore multimediale è entrato in uno stato del lettore tracciato.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 1%
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

>[!TAB Edge Roku]

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

>[!TAB Roku 2.x]

Il tracciamento dello stato del lettore non è disponibile nel SDK Roku 2.x. Per tenere traccia degli stati del lettore, utilizza [Roku Edge SDK](/help/implementation/edge/roku.md).

>[!TAB API Media Collection]

Invia un POST `stateStart` all&#39;endpoint [eventi](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

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
