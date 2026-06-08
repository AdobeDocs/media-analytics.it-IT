---
title: Sottotitoli codificati
description: Monitora quando il visualizzatore attiva e disattiva i sottotitoli in modo che il backend possa creare rapporti sul coinvolgimento dei sottotitoli.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 2%

---


# Sottotitoli codificati

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per lo stato **Sottotitoli**del lettore. Vedi [Flussi interessati dai sottotitoli](/help/reporting/metrics/closed-captioning-streams-impacted.md), [Conteggi sottotitoli](/help/reporting/metrics/closed-captioning-count.md) e [Durata totale sottotitoli](/help/reporting/metrics/closed-captioning-total-duration.md) per le metriche di reporting corrispondenti.*

>[!ENDSHADEBOX]

Lo stato del lettore di sottotitoli codificati tiene traccia di quando il visualizzatore attiva e disattiva i sottotitoli. Attiva un evento di inizio stato quando le didascalie sono abilitate e un evento di fine stato quando le didascalie sono disabilitate. Il backend calcola tre metriche da questi eventi: flussi interessati, numero di voci di stato e tempo totale nello stato.

| Proprietà | Valore |
| --- | --- |
| **Variabili di dati di contesto** | `a.media.states.closedcaptioning.set`, `a.media.states.closedcaptioning.count`, `a.media.states.closedcaptioning.time` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) e [`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) (voci con `name: "closedCaptioning"`) |
| **Caratteristiche Audience Manager** | `c_contextdata.a.media.states.closedcaptioning.set`, `c_contextdata.a.media.states.closedcaptioning.count`, `c_contextdata.a.media.states.closedcaptioning.time` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio stato](/help/implementation/events/player-state/state-start.md), [fine stato](/help/implementation/events/player-state/state-end.md) |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Utilizza [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview) per inviare un evento `media.statesUpdate` con lo stato aggiunto a `statesStart`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "closedCaptioning" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Quando il visualizzatore disabilita i sottotitoli, invia un altro evento con lo stato in `statesEnd`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "closedCaptioning" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

Utilizzare `tracker.trackPlayerStateStart()` e `tracker.trackPlayerStateEnd()` con la costante `MediaConstants.PlayerState.CLOSED_CAPTION`.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.CLOSED_CAPTION)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

Utilizzare `tracker.trackPlayerStateStart()` e `tracker.trackPlayerStateEnd()` con la costante `MediaConstants.PlayerState.CLOSED_CAPTION`.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.CLOSED_CAPTION)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Edge Roku]

Utilizza `sendMediaEvent` per inviare un evento `media.statesUpdate` con lo stato aggiunto a `statesStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "closedCaptioning" }],
            "playhead": 60
        }
    }
})
```

Quando il visualizzatore disabilita i sottotitoli, invia un altro evento con lo stato in `statesEnd`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "closedCaptioning" }],
            "playhead": 90
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) con `closedCaptioning` in `statesStart` (o `statesEnd` quando il visualizzatore disabilita i sottotitoli):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "closedCaptioning" }],
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

Usa `ADB.Media.createStateObject` e la costante `ADB.Media.PlayerState.ClosedCaptioning`:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.ClosedCaptioning);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

Utilizza `ADBMobile.media.createStateObject` direttamente con la stringa `"closedCaptioning"`, in quanto Chromecast non ha costanti con nome `PlayerState`:

```javascript
var stateObject = ADBMobile.media.createStateObject("closedCaptioning");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the viewer disables captions:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

Il tracciamento dello stato del lettore non è disponibile nel SDK Roku 2.x. Per tenere traccia degli stati del lettore, utilizza [Roku Edge SDK](/help/implementation/edge/roku.md).

>[!TAB API Media Collection]

Invia una richiesta POST `stateStart` quando i sottotitoli sono abilitati e un POST `stateEnd` quando sono disabilitati:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "closedCaptioning"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).

>[!ENDTABS]
