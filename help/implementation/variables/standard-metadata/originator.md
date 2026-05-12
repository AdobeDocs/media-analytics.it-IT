---
title: Iniziatore
description: Imposta il creatore o lo studio di produzione del contenuto.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 8%

---


# Iniziatore

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Originator**. Vedi [Iniziatore](/help/reporting/dimensions/originator.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile del creatore è il creatore o lo studio di produzione del contenuto (ad esempio, `"Warner Brothers"`, `"Sony"` o `"Disney"`). Utilizzalo per confrontare il coinvolgimento tra proprietari di contenuti o titolari di diritti.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.originator` |
| **Campo raccolta XDM** | [`mediaCollection.sessionDetails.originator`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obbligatorio** | No |
| **Inviato con** | Avvio della sessione, chiusura della sessione |

## Web SDK

Imposta `originator` all&#39;interno di `mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        originator: "Warner Brothers"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Passa il creatore come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.ORIGINATOR`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.ORIGINATOR] = "Warner Brothers"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Cotlino)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.ORIGINATOR] = "Warner Brothers"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilizza `createMediaSession` per impostare `originator` in `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "originator": "Warner Brothers"
            },
            "playhead": 0
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `originator` in `mediaCollection.sessionDetails`:

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
          "channel": "Sports",
          "originator": "Warner Brothers"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Passa il mittente nell&#39;oggetto `contextData` utilizzando `ADB.Media.VideoMetadataKeys.Originator`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Originator] = "Warner Brothers";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Includi `media.originator` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.originator": "Warner Brothers"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).
