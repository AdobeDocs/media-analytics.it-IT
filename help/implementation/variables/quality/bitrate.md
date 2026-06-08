---
title: Bitrate
description: Imposta il bitrate di riproduzione corrente (in kbps) sull'oggetto QoE in modo che il backend possa calcolare le metriche del bitrate.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 2%

---


# Bitrate

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Bitrate**. Vedere [[!UICONTROL Average bitrate] (dimensione)](/help/reporting/dimensions/average-bitrate.md) e [[!UICONTROL Average bitrate] (metrica)](/help/reporting/metrics/average-bitrate.md) per le variabili di reporting corrispondenti.*

>[!ENDSHADEBOX]

La variabile bitrate è il bitrate di riproduzione corrente, espresso in kilobit al secondo. Impostatelo sull&#39;oggetto QoE ogni volta che il lettore negozia un bitrate, e aggiornate l&#39;oggetto QoE quando il bitrate cambia. Il back-end utilizza i valori del bitrate per calcolare [[!UICONTROL Average bitrate]](/help/reporting/metrics/average-bitrate.md), la dimensione del bucket per bitrate e la metrica [[!UICONTROL Bitrate changes]](/help/reporting/metrics/bitrate-changes.md).

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.qoe.bitrateAverageBucket` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.qoeDataDetails.bitrate`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.qoe.bitrateAverageBucket` |
| **Obbligatorio** | No |
| **Inviato con** | Eventi di qualità ([modifica bitrate](/help/implementation/events/playback/bitrate-change.md), [avvio buffer](/help/implementation/events/playback/buffer-start.md), [errore](/help/implementation/events/error.md)), chiusura sessione |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `bitrate` all&#39;interno di `xdm.mediaCollection.qoeDataDetails` il `media.bitrateChange` (o qualsiasi evento relativo alla qualità) durante la chiamata a [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

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

Passa il bitrate come primo argomento a `createQoEObject`. Aggiorna l’oggetto QoE sul tracciatore prima che venga attivato qualsiasi evento di qualità.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Passa il bitrate come primo argomento a `createQoEObject`. Aggiorna l’oggetto QoE sul tracciatore prima che venga attivato qualsiasi evento di qualità.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Edge Roku]

Impostare `bitrate` all&#39;interno di `xdm.mediaCollection.qoeDataDetails` quando si chiama `sendMediaEvent` per eventi di qualità come `media.bitrateChange`:

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

Chiama l&#39;endpoint [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) con `bitrate` all&#39;interno di `xdm.mediaCollection.qoeDataDetails`:

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

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

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

>[!TAB Chromecast]

Passa il bitrate in kbps come primo argomento a `ADBMobile.media.createQoSObject` e aggiorna il tracciatore:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate (kbps)
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Roku 2.x]

Passa il bitrate in kbps come primo argomento a `adb_media_init_qosinfo` e aggiorna il tracciatore con `mediaUpdateQoS`:

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
```

>[!TAB API Media Collection]

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

>[!ENDTABS]
