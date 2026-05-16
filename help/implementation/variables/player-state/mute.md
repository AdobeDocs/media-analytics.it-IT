---
title: Disattiva audio
description: Monitora quando il visualizzatore disattiva e riattiva l’audio in modo che il backend possa segnalare il coinvolgimento della disattivazione audio.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 5%

---


# Disattiva audio

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per lo stato **Disattiva audio**del lettore. Vedi [Flussi interessati dalla disattivazione audio](/help/reporting/metrics/mute-streams-impacted.md), [Conteggi disattivazione audio](/help/reporting/metrics/mute-count.md) e [Durata totale disattivazione audio](/help/reporting/metrics/mute-total-duration.md) per le metriche di reporting corrispondenti.*

>[!ENDSHADEBOX]

Lo stato di disattivazione audio del lettore registra quando il visualizzatore disattiva e riattiva l’audio. Attiva un evento di inizio stato quando il visualizzatore disattiva l’audio e un evento di fine stato quando il visualizzatore disattiva l’audio. Il backend calcola tre metriche da questi eventi: flussi interessati, numero di voci di stato e tempo totale nello stato.

| Proprietà | Valore |
| --- | --- |
| **Variabili di dati di contesto** | `a.media.states.mute.set`, `a.media.states.mute.count`, `a.media.states.mute.time` |
| **Campo raccolta XDM** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) e [`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) (voci con `name: "mute"`) |
| **Caratteristiche Audience Manager** | `c_contextdata.a.media.states.mute.set`, `c_contextdata.a.media.states.mute.count`, `c_contextdata.a.media.states.mute.time` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio stato](/help/implementation/events/player-state/state-start.md), [fine stato](/help/implementation/events/player-state/state-end.md) |

## Web SDK

Utilizza [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview) per inviare un evento `media.statesUpdate` con lo stato aggiunto a `statesStart`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Quando il visualizzatore smette di funzionare, invia un altro evento con lo stato in `statesEnd`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "mute" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

Utilizzare `tracker.trackPlayerStateStart()` e `tracker.trackPlayerStateEnd()` con la costante `MediaConstants.PlayerState.MUTE`.

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.MUTE)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Cotlino)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.MUTE)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

## Roku (BrightScript)

Utilizza `sendMediaEvent` per inviare un evento `media.statesUpdate` con lo stato aggiunto a `statesStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "mute" }],
            "playhead": 60
        }
    }
})
```

Quando il visualizzatore smette di funzionare, invia un altro evento con lo stato in `statesEnd`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "mute" }],
            "playhead": 90
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) con `mute` in `statesStart` (o `statesEnd` quando il visualizzatore annulla l&#39;audio):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "mute" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## Media SDK

Usa `ADB.Media.createStateObject` e la costante `ADB.Media.PlayerState.Mute`:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## API Media Collection

Invia una richiesta POST `stateStart` quando il visualizzatore disattiva l&#39;audio e un POST `stateEnd` quando l&#39;audio viene disattivato:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).
