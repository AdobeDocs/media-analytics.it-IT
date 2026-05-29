---
title: In focus
description: Monitora quando il lettore è a fuoco sullo schermo del visualizzatore in modo che il backend possa segnalare il coinvolgimento a fuoco.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 2%

---


# In focus

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per lo stato del lettore **In focus**. Vedi [Flussi interessati da in focus](/help/reporting/metrics/in-focus-streams-impacted.md), [Conteggi in focus](/help/reporting/metrics/in-focus-count.md) e [Durata totale in focus](/help/reporting/metrics/in-focus-total-duration.md) per le metriche di reporting corrispondenti.*

>[!ENDSHADEBOX]

Lo stato in focus del lettore tiene traccia di quando il lettore ha l’attenzione dell’utente. Attiva un evento di inizio stato quando il lettore diventa attivo (in genere quando la scheda o la finestra del lettore diventa attiva) e un evento di fine stato quando il lettore perde lo stato attivo. Il backend calcola tre metriche da questi eventi: flussi interessati, numero di voci di stato e tempo totale nello stato.

| Proprietà | Valore |
| --- | --- |
| **Variabili di dati di contesto** | `a.media.states.infocus.set`, `a.media.states.infocus.count`, `a.media.states.infocus.time` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) e [`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) (voci con `name: "inFocus"`) |
| **Caratteristiche Audience Manager** | `c_contextdata.a.media.states.infocus.set`, `c_contextdata.a.media.states.infocus.count`, `c_contextdata.a.media.states.infocus.time` |
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
      statesStart: [{ name: "inFocus" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Quando il lettore perde lo stato attivo, invia un altro evento con lo stato in `statesEnd`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "inFocus" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

Utilizzare `tracker.trackPlayerStateStart()` e `tracker.trackPlayerStateEnd()` con la costante `MediaConstants.PlayerState.IN_FOCUS`.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.IN_FOCUS)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

Utilizzare `tracker.trackPlayerStateStart()` e `tracker.trackPlayerStateEnd()` con la costante `MediaConstants.PlayerState.IN_FOCUS`.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.IN_FOCUS)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Roku]

Utilizza `sendMediaEvent` per inviare un evento `media.statesUpdate` con lo stato aggiunto a `statesStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "inFocus" }],
            "playhead": 60
        }
    }
})
```

Quando il lettore perde lo stato attivo, invia un altro evento con lo stato in `statesEnd`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "inFocus" }],
            "playhead": 90
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) con `inFocus` in `statesStart` (o `statesEnd` quando il lettore perde lo stato attivo):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "inFocus" }],
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

Usa `ADB.Media.createStateObject` e la costante `ADB.Media.PlayerState.InFocus`:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.InFocus);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

Utilizza `ADBMobile.media.createStateObject` direttamente con la stringa `"inFocus"`, in quanto Chromecast non ha costanti con nome `PlayerState`:

```javascript
var stateObject = ADBMobile.media.createStateObject("inFocus");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the player loses focus:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB API Media Collection]

Invia una richiesta POST `stateStart` quando il lettore diventa attivo e un POST `stateEnd` quando perde lo stato attivo:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "inFocus"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).

>[!ENDTABS]
