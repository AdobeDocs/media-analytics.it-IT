---
title: Bitrate
description: Imposta il bitrate di riproduzione corrente (in kbps) sull'oggetto QoE in modo che il backend possa calcolare le metriche del bitrate.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 4%

---


# Bitrate

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Bitrate**. Vedi [Bitrate medio (dimensione)](/help/reporting/dimensions/average-bitrate.md) e [Bitrate medio (metrica)](/help/reporting/metrics/average-bitrate.md) per le variabili di reporting corrispondenti.*

>[!ENDSHADEBOX]

La variabile bitrate è il bitrate di riproduzione corrente, espresso in kilobit al secondo. Impostatelo sull&#39;oggetto QoE ogni volta che il lettore negozia un bitrate, e aggiornate l&#39;oggetto QoE quando il bitrate cambia. Il backend utilizza i valori del bitrate per calcolare il bitrate medio, la dimensione del bucket per bitrate e la metrica delle modifiche del bitrate.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.qoe.bitrateAverageBucket` |
| **Campo raccolta XDM** | [`mediaCollection.qoeDataDetails.bitrate`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Obbligatorio** | No |
| **Inviato con** | Eventi di qualità (modifica del bitrate, buffer, errore), chiusura della sessione |

## Web SDK

Imposta `bitrate` all&#39;interno di `mediaCollection.qoeDataDetails` il `media.bitrateChange` (o qualsiasi evento relativo alla qualità) durante la chiamata a [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

Passa il bitrate come primo argomento a `createQoEObject`. Aggiorna l’oggetto QoE sul tracciatore prima che venga attivato qualsiasi evento di qualità.

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

Impostare `bitrate` all&#39;interno di `mediaCollection.qoeDataDetails` quando si chiama `sendMediaEvent` per eventi di qualità come `media.bitrateChange`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 90
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) con `bitrate` all&#39;interno di `mediaCollection.qoeDataDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## Media SDK

Passa il bitrate come primo argomento a `ADB.Media.createQoEObject` e aggiorna il tracker:

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
```

## API Media Collection

Includi `media.qoe.bitrate` nell&#39;oggetto `params` della richiesta POST `bitrateChange`:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 3200
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).
