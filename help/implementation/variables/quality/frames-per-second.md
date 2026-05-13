---
title: Fotogrammi al secondo
description: Imposta la frequenza fotogrammi corrente sull'oggetto QoE in modo che il backend abbia un contesto di frequenza fotogrammi per il reporting di qualità.
feature: Streaming Media
role: Developer
source-git-commit: 0e6b5a8ef5738191276976ed31125016774c043d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 5%

---


# Fotogrammi al secondo

La variabile frame al secondo corrisponde al frame rate corrente del flusso. Impostatelo sull&#39;oggetto QoE insieme al bitrate e ai fotogrammi saltati in modo che il backend abbia un contesto di qualità completa per ogni sessione di riproduzione. Adobe Analytics non crea automaticamente una variabile di reporting per il frame rate; crea una regola di elaborazione personalizzata se desideri che venga visualizzata come un rapporto.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | Nessuno (Adobe Analytics non assegna una chiave di dati contestuali riservata per il frame rate) |
| **Campo raccolta XDM** | [`mediaCollection.qoeDataDetails.framesPerSecond`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Obbligatorio** | No |
| **Inviato con** | Eventi di qualità, chiusura sessione |

## Web SDK

Imposta `framesPerSecond` all&#39;interno di `mediaCollection.qoeDataDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        framesPerSecond: 24
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

Passa la frequenza fotogrammi come terzo argomento (`fps`) a `createQoEObject`.

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android (Cotlino)**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

## Roku (BrightScript)

Imposta `framesPerSecond` in `mediaCollection.qoeDataDetails` quando chiama `sendMediaEvent`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "framesPerSecond": 24
            },
            "playhead": 90
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) con `framesPerSecond` all&#39;interno di `mediaCollection.qoeDataDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "framesPerSecond": 24
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## Media SDK

Passa la frequenza fotogrammi come terzo argomento a `ADB.Media.createQoEObject`:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
```

## API Media Collection

Includi `media.qoe.framesPerSecond` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.framesPerSecond": 24
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).
