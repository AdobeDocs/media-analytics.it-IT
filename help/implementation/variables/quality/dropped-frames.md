---
title: Fotogrammi persi
description: Imposta il conteggio corrente dei fotogrammi saltati sull'oggetto QoE in modo che il backend possa riportare la qualità del rilascio dei fotogrammi.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 2%

---


# Fotogrammi persi

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Dropped frames**. Vedi [Fotogrammi saltati](/help/reporting/dimensions/dropped-frames.md) per la dimensione e la metrica di reporting corrispondenti.*

>[!ENDSHADEBOX]

La variabile dei fotogrammi saltati è il conteggio corrente dei fotogrammi saltati dal lettore durante la sessione. Impostalo sull’oggetto QoE e aggiorna il valore ogni volta che il lettore segnala nuove cadute. Il backend riporta il valore più recente alla chiusura della sessione.

>[!NOTE]
>
>Passa sempre il **totale cumulativo** dei fotogrammi saltati per l&#39;intera sessione fino a quel punto, non un delta per intervallo. Se si reimposta il valore su `0` tra gli aggiornamenti, il backend riceve `0` come valore finale e segnala zero fotogrammi saltati per la sessione indipendentemente da ciò che è stato effettivamente saltato in precedenza.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.qoe.droppedFrameCount` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.qoe.droppedFrameCount` |
| **Obbligatorio** | No |
| **Inviato con** | Eventi di qualità ([modifica bitrate](/help/implementation/events/playback/bitrate-change.md), [avvio buffer](/help/implementation/events/playback/buffer-start.md), [errore](/help/implementation/events/error.md)), chiusura sessione |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `droppedFrames` all&#39;interno di `xdm.mediaCollection.qoeDataDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview):

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

>[!TAB iOS]

Passa i fotogrammi saltati come quarto argomento a `createQoEObject`. Aggiorna il tracciatore prima che venga attivato qualsiasi evento di qualità.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 3)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Passa i fotogrammi saltati come quarto argomento a `createQoEObject`. Aggiorna il tracciatore prima che venga attivato qualsiasi evento di qualità.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      3L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Edge Roku]

Imposta `droppedFrames` in `xdm.mediaCollection.qoeDataDetails` quando chiama `sendMediaEvent`:

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

>[!TAB API Media Edge]

Chiama l&#39;endpoint [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) con `droppedFrames` all&#39;interno di `xdm.mediaCollection.qoeDataDetails`:

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

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Passa i fotogrammi saltati come quarto argomento a `ADB.Media.createQoEObject`:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 3);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

Passa il conteggio cumulativo dei fotogrammi saltati come quarto argomento a `ADBMobile.media.createQoSObject` e aggiorna il tracciatore:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate
  0,     // startupTime
  24,    // fps
  0      // droppedFrames (cumulative total)
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Roku 2.x]

Passa il conteggio cumulativo dei fotogrammi saltati come quarto argomento (`droppedFrames`) a `adb_media_init_qosinfo` e aggiorna il tracciatore con `mediaUpdateQoS`:

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
```

>[!TAB API Media Collection]

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

>[!ENDTABS]
