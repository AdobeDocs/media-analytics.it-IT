---
title: Modifica bitrate
description: Segnala che il bitrate di riproduzione è cambiato.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 2%

---


# Modifica bitrate

L’evento di modifica del bitrate segnala che il lettore ha negoziato un nuovo bitrate di riproduzione. Invia ogni volta che il bitrate cambia durante la riproduzione. Includere il nuovo valore bitrate nei dati QoE in modo che il backend possa calcolare [[!UICONTROL Average bitrate]](/help/reporting/metrics/average-bitrate.md) e la dimensione bucket per bitrate.

* **Prerequisiti**: [Inizio sessione](../session/session-start.md)
* **Metrica associata**: [[!UICONTROL Bitrate changes]](/help/reporting/metrics/bitrate-changes.md)

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.bitrateChange"` e il nuovo bitrate in `qoeDataDetails`:

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

>[!TAB iOS]

Crea un oggetto QoE con il nuovo bitrate e aggiorna il tracciatore prima che venga attivato l’evento di modifica del bitrate.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

>[!TAB Android]

Crea un oggetto QoE con il nuovo bitrate e aggiorna il tracciatore prima che venga attivato l’evento di modifica del bitrate.

```kotlin
val qoeObject = Media.createQoEObject(3200, 0, 24, 0)

tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

>[!TAB Roku]

Chiamare `sendMediaEvent` con `eventType: "media.bitrateChange"` e il nuovo bitrate in `qoeDataDetails`:

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

>[!TAB API Media Edge]

Chiama l&#39;endpoint [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/) con il nuovo bitrate in `qoeDataDetails`:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bitrateChange?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
        },
        "sessionID": "{sid}",
        "playhead": 90
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Crea un oggetto QoE con il nuovo bitrate e aggiorna il tracciatore:

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

>[!TAB Chromecast]

Aggiorna l&#39;oggetto QoS restituito dal delegato `getQoSObject`, quindi tieni traccia dell&#39;evento:

```javascript
// Update QoS data via the delegate
this._qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate (kbps)
  0,     // dropped frames
  24,    // fps
  0      // startup time
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
```

>[!TAB API Media Collection]

Invia un POST `bitrateChange` all&#39;endpoint [events](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) con il nuovo bitrate in `qoeData`:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "qoeData": {
    "media.qoe.bitrate": 3200
  }
}
```

>[!ENDTABS]
