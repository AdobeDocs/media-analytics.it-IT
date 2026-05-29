---
title: Tempo di avvio
description: Imposta il tempo di avvio del lettore, in millisecondi, in modo che il backend possa riportare la qualità del tempo al primo fotogramma.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 2%

---


# Tempo di avvio

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Time to start**. Vedere [[!UICONTROL Time to start]](/help/reporting/dimensions/time-to-start.md) per la dimensione e la metrica di reporting corrispondenti.*

>[!ENDSHADEBOX]

La variabile &quot;time to start&quot; è il tempo trascorso, in millisecondi, tra l’avvio della riproduzione da parte del lettore e il rendering del primo fotogramma. Impostatelo sull&#39;oggetto QoE prima che venga attivato l&#39;evento di inizio sessione. Adobe memorizza e segnala il valore in secondi, passa millisecondi e Adobe converte al momento dell’acquisizione.

>[!IMPORTANT]
>
>Una volta che il lettore inizia il rendering dei fotogrammi di contenuto, interrompi l&#39;aggiornamento di `timeToStart`. Il valore può aumentare durante la fase di buffering iniziale o di caricamento, ma deve essere trattato come fisso nel momento in cui inizia la riproduzione. Continuando ad aggiornarla dopo il rendering del primo fotogramma, si produce una metrica [[!UICONTROL Time to start]](/help/reporting/metrics/time-to-start.md) gonfiata o errata.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.qoe.timeToStart` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.qoe.timeToStart` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md), chiusura sessione |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `timeToStart` all&#39;interno di `xdm.mediaCollection.qoeDataDetails` su `media.sessionStart` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      qoeDataDetails: {
        timeToStart: 30000
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passa l&#39;ora di avvio come secondo argomento (`startupTime`) a `createQoEObject`.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 30000,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Passa l&#39;ora di avvio come secondo argomento (`startupTime`) a `createQoEObject`.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      30000.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku]

Imposta `timeToStart` all&#39;interno di `xdm.mediaCollection.qoeDataDetails` su `media.sessionStart` durante la chiamata a `createMediaSession`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "qoeDataDetails": {
                "timeToStart": 30000
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `timeToStart` in `xdm.mediaCollection.qoeDataDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports"
        },
        "qoeDataDetails": {
          "timeToStart": 30000
        },
        "playhead": 0
      }
    }
  }]
}
```

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Passare il tempo per iniziare come secondo argomento a `ADB.Media.createQoEObject`:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 30000, 24, 0);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

Passare il tempo di avvio in millisecondi come secondo argomento (`startupTime`) a `ADBMobile.media.createQoSObject` e aggiornare il tracker:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,   // bitrate
  0,      // startupTime (ms)
  24,     // fps
  0       // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB API Media Collection]

Includi `media.qoe.timeToStart` nell&#39;oggetto `params` in `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.qoe.timeToStart": 30000
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).

>[!ENDTABS]
