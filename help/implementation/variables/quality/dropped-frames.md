---
title: Fotogrammi persi
description: Imposta il conteggio corrente dei fotogrammi saltati sull'oggetto QoE in modo che il backend possa riportare la qualità del rilascio dei fotogrammi.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 5%

---


# Fotogrammi persi

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Dropped frames**. Vedi [Fotogrammi saltati](/help/reporting/dimensions/dropped-frames.md) per la dimensione e la metrica di reporting corrispondenti.*

>[!ENDSHADEBOX]

La variabile dei fotogrammi saltati è il conteggio corrente dei fotogrammi saltati dal lettore durante la sessione. Impostalo sull’oggetto QoE e aggiorna il valore ogni volta che il lettore segnala nuove cadute. Il backend riporta il valore più recente alla chiusura della sessione.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.qoe.droppedFrameCount` |
| **Campo raccolta XDM** | [`mediaCollection.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Obbligatorio** | No |
| **Inviato con** | Eventi di qualità, chiusura sessione |

## Web SDK

Imposta `droppedFrames` all&#39;interno di `mediaCollection.qoeDataDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 3
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

Passa i fotogrammi saltati come quarto argomento a `createQoEObject`. Aggiorna il tracciatore prima che venga attivato qualsiasi evento di qualità.

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 3)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android (Cotlino)**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      3L)

tracker.updateQoEObject(qoeObject)
```

## Roku (BrightScript)

Imposta `droppedFrames` in `mediaCollection.qoeDataDetails` quando chiama `sendMediaEvent`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 3
            },
            "playhead": 90
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) con `droppedFrames` all&#39;interno di `mediaCollection.qoeDataDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "droppedFrames": 3
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## Media SDK

Passa i fotogrammi saltati come quarto argomento a `ADB.Media.createQoEObject`:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 3);
tracker.updateQoEObject(qoeObject);
```

## API Media Collection

Includi `media.qoe.droppedFrames` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.droppedFrames": 3
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).
