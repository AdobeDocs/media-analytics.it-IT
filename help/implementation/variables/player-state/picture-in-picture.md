---
title: Immagine nell’immagine
description: Monitora quando il visualizzatore entra ed esce dalla riproduzione picture-in-picture in modo che il backend possa riportare il coinvolgimento PiP.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 4%

---


# Immagine nell’immagine

>[!BEGINSHADEBOX]

*Questa pagina contiene informazioni sulla raccolta dati per lo stato del lettore **Immagine nell&#39;immagine**. Vedi [Flussi interessati da immagine nell&#39;immagine](/help/reporting/metrics/picture-in-picture-streams-impacted.md), [Conteggi immagine nell&#39;immagine](/help/reporting/metrics/picture-in-picture-count.md) e [Durata totale immagine nell&#39;immagine](/help/reporting/metrics/picture-in-picture-total-duration.md) per le metriche di reporting corrispondenti.*

>[!ENDSHADEBOX]

Lo stato di picture-in-picture del lettore tiene traccia di quando il visualizzatore entra ed esce dalla riproduzione picture-in-picture. Attiva un evento di inizio stato quando inizia l&#39;immagine nell&#39;immagine e un evento di fine stato quando termina. Il backend calcola tre metriche da questi eventi: flussi interessati, numero di voci di stato e tempo totale nello stato.

| Proprietà | Valore |
| --- | --- |
| **Variabili di dati di contesto** | `a.media.states.pictureinpicture.set`, `a.media.states.pictureinpicture.count`, `a.media.states.pictureinpicture.time` |
| **Campo raccolta XDM** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/media-collection-details) e [`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/media-collection-details) (voci con `name: "pictureInPicture"`) |
| **Caratteristiche Audience Manager** | `c_contextdata.a.media.states.pictureinpicture.set`, `c_contextdata.a.media.states.pictureinpicture.count`, `c_contextdata.a.media.states.pictureinpicture.time` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio stato](/help/implementation/events/player-state/state-start.md), [fine stato](/help/implementation/events/player-state/state-end.md) |

## Web SDK

Utilizza [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview) per inviare un evento `media.statesUpdate` con lo stato aggiunto a `statesStart`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Quando il visualizzatore esce dall&#39;immagine nell&#39;immagine, invia un altro evento con lo stato in `statesEnd`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

Utilizzare `tracker.trackPlayerStateStart()` e `tracker.trackPlayerStateEnd()` con la costante `MediaConstants.PlayerState.PICTURE_IN_PICTURE`.

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.PICTURE_IN_PICTURE)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Cotlino)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.PICTURE_IN_PICTURE)

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
            "statesStart": [{ "name": "pictureInPicture" }],
            "playhead": 60
        }
    }
})
```

Quando il visualizzatore esce dall&#39;immagine nell&#39;immagine, invia un altro evento con lo stato in `statesEnd`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "pictureInPicture" }],
            "playhead": 90
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) con `pictureInPicture` in `statesStart` (o `statesEnd` quando il visualizzatore esce da PiP):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "pictureInPicture" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## Media SDK

Usa `ADB.Media.createStateObject` e la costante `ADB.Media.PlayerState.PictureInPicture`:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.PictureInPicture);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## API Media Collection

Invia una richiesta POST `stateStart` all&#39;inizio dell&#39;immagine nell&#39;immagine e un POST `stateEnd` alla fine:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "pictureInPicture"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).
