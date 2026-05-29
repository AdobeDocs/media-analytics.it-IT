---
title: Fotogrammi al secondo
description: Imposta la frequenza fotogrammi corrente sull'oggetto QoE in modo che il backend abbia un contesto di frequenza fotogrammi per il reporting di qualità.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 3%

---


# Fotogrammi al secondo

La variabile frame al secondo corrisponde al frame rate corrente del flusso. Impostatelo sull&#39;oggetto QoE insieme al bitrate e ai fotogrammi saltati in modo che il backend abbia un contesto di qualità completa per ogni sessione di riproduzione. Adobe Analytics non crea automaticamente una variabile di reporting per il frame rate; crea una regola di elaborazione personalizzata se desideri che venga visualizzata come un rapporto.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | Nessuno (Adobe Analytics non assegna una chiave di dati contestuali riservata per il frame rate) |
| **Campo raccolta XDM** | [`xdm.mediaCollection.qoeDataDetails.framesPerSecond`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Caratteristica Audience Manager** | N/D |
| **Obbligatorio** | No |
| **Inviato con** | Eventi di qualità ([modifica bitrate](/help/implementation/events/playback/bitrate-change.md), [avvio buffer](/help/implementation/events/playback/buffer-start.md), [errore](/help/implementation/events/error.md)), chiusura sessione |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `framesPerSecond` all&#39;interno di `xdm.mediaCollection.qoeDataDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

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

>[!TAB iOS]

Passa la frequenza fotogrammi come terzo argomento (`fps`) a `createQoEObject`.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Passa la frequenza fotogrammi come terzo argomento (`fps`) a `createQoEObject`.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku]

Imposta `framesPerSecond` in `xdm.mediaCollection.qoeDataDetails` quando chiama `sendMediaEvent`:

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

>[!TAB API Media Edge]

Chiama l&#39;endpoint [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) con `framesPerSecond` all&#39;interno di `xdm.mediaCollection.qoeDataDetails`:

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

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Passa la frequenza fotogrammi come terzo argomento a `ADB.Media.createQoEObject`:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

Passa la frequenza fotogrammi come terzo argomento (`fps`) a `ADBMobile.media.createQoSObject` e aggiorna il tracciatore:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB API Media Collection]

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

>[!ENDTABS]
