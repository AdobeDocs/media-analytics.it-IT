---
title: A schermo intero
description: Monitora quando il visualizzatore entra ed esce dalla riproduzione a schermo intero, in modo che il backend possa riportare il coinvolgimento a schermo intero.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 3%

---


# A schermo intero

>[!BEGINSHADEBOX]

*In questa pagina è illustrata la raccolta dati per lo stato del lettore **Schermo intero**. Vedi [Flussi interessati dalla visualizzazione a schermo intero](/help/reporting/metrics/full-screen-streams-impacted.md), [Conteggi a schermo intero](/help/reporting/metrics/full-screen-count.md) e [Durata totale a schermo intero](/help/reporting/metrics/full-screen-total-duration.md) per le metriche di reporting corrispondenti.*

>[!ENDSHADEBOX]

Lo stato a schermo intero del lettore tiene traccia di quando il visualizzatore entra ed esce dalla riproduzione a schermo intero. Attiva un evento di inizio stato ogni volta che il visualizzatore entra a schermo intero e un evento di fine stato quando il visualizzatore esce. Il backend calcola tre metriche da questi eventi: flussi interessati, numero di voci di stato e tempo totale nello stato.

| Proprietà | Valore |
| --- | --- |
| **Variabili di dati di contesto** | `a.media.states.fullscreen.set`, `a.media.states.fullscreen.count`, `a.media.states.fullscreen.time` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/media-collection-details) e [`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/media-collection-details) (voci con `name: "fullscreen"`) |
| **Caratteristiche Audience Manager** | `c_contextdata.a.media.states.fullscreen.set`, `c_contextdata.a.media.states.fullscreen.count`, `c_contextdata.a.media.states.fullscreen.time` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio stato](/help/implementation/events/player-state/state-start.md), [fine stato](/help/implementation/events/player-state/state-end.md) |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Utilizza [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview) per inviare un evento `media.statesUpdate` con lo stato aggiunto a `statesStart`:

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

Quando il visualizzatore esce dalla modalità a schermo intero, invia un altro evento con lo stato in `statesEnd`:

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

>[!TAB iOS]

Utilizzare `tracker.trackPlayerStateStart()` e `tracker.trackPlayerStateEnd()` con la costante `MediaConstants.PlayerState.FULLSCREEN`.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(info: stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

Utilizzare `tracker.trackPlayerStateStart()` e `tracker.trackPlayerStateEnd()` con la costante `MediaConstants.PlayerState.FULLSCREEN`.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Edge Roku]

Utilizza `sendMediaEvent` per inviare un evento `media.statesUpdate` con lo stato aggiunto a `statesStart`:

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

Quando il visualizzatore esce dalla modalità a schermo intero, invia un altro evento con lo stato in `statesEnd`:

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

>[!TAB API Media Edge]

Chiama l&#39;endpoint [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) con `fullscreen` in `statesStart` (o `statesEnd` quando il visualizzatore esce):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "fullscreen" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Usa `ADB.Media.createStateObject` e la costante `ADB.Media.PlayerState.FullScreen`:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);

tracker.trackPlayerStateStart(stateObject);
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

Utilizza `ADBMobile.media.createStateObject` direttamente con la stringa `"fullscreen"`, in quanto Chromecast non ha costanti con nome `PlayerState`:

```javascript
var stateObject = ADBMobile.media.createStateObject("fullscreen");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the user exits full-screen:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

Il tracciamento dello stato del lettore non è disponibile nel SDK Roku 2.x. Per tenere traccia degli stati del lettore, utilizza [Roku Edge SDK](/help/implementation/edge/roku.md).

>[!TAB API Media Collection]

Invia una richiesta POST `stateStart` quando il visualizzatore entra a schermo intero e un POST `stateEnd` quando escono:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523850000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).

>[!ENDTABS]
