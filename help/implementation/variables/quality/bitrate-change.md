---
title: Modifica bitrate
description: Attiva un evento di modifica del bitrate ogni volta che il lettore passa a un bitrate diverso.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 5%

---


# Modifica bitrate

>[!BEGINSHADEBOX]

*In questa pagina viene illustrato come implementare gli eventi di modifica del bitrate. Vedi [Modifiche bitrate (dimensione)](/help/reporting/dimensions/bitrate-changes.md) e [Modifiche bitrate (metrica)](/help/reporting/metrics/bitrate-changes.md) per le variabili di reporting corrispondenti.*

>[!ENDSHADEBOX]

L’evento di modifica del bitrate segnala che il lettore è passato a un bitrate diverso. Aggiorna prima il valore [Bitrate](/help/implementation/variables/quality/bitrate.md) nell&#39;oggetto QoE, quindi attiva l&#39;evento di modifica del bitrate. Il backend utilizza il conteggio di questi eventi per calcolare la dimensione e la metrica delle modifiche del bitrate, e i valori del bitrate risultanti vengono inseriti nel valore Bitrate medio.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | (nessuno — conteggiato dal backend) |
| **Tipo di evento XDM** | `media.bitrateChange` |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.qoe.bitrateChangeCount` |
| **Obbligatorio** | No |
| **Inviato con** | [Modifica bitrate](/help/implementation/events/playback/bitrate-change.md) |

## Web SDK

Utilizza [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview) per inviare un evento `media.bitrateChange` con il nuovo bitrate:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 4500,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 120
    }
  }
});
```

## Mobile SDK

Aggiorna l’oggetto QoE con il nuovo bitrate, quindi attiva l’evento di modifica del bitrate.

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 4500,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)
tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

**Android (Cotlino)**

```kotlin
val qoeObject = Media.createQoEObject(4500L, 0.0, 24.0, 0L)
tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

## Roku (BrightScript)

Utilizza `sendMediaEvent` con `media.bitrateChange` per segnalare una modifica del bitrate. Includi il nuovo bitrate in `qoeDataDetails`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 4500,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 120
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) con `qoeDataDetails` aggiornato:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 4500
        },
        "sessionID": "{sid}",
        "playhead": 120
      }
    }
  }]
}
```

## Media SDK

Aggiorna l’oggetto QoE e attiva l’evento:

```javascript
var qoeObject = ADB.Media.createQoEObject(4500, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

## API Media Collection

Invia una richiesta POST `bitrateChange` con il nuovo bitrate:

```json
{
  "playerTime": { "playhead": 120, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 4500
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).
