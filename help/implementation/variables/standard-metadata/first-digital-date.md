---
title: Data prima versione digitale
description: Imposta la data in cui il contenuto è andato in onda per la prima volta su una piattaforma digitale. Adobe consiglia il formato AAAA-MM-GG.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 8%

---


# Data prima versione digitale

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **First digital date**. Vedi [Prima data digitale](/help/reporting/dimensions/first-digital-date.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La prima variabile digitale di data è la data in cui il contenuto è andato in onda per la prima volta su qualsiasi piattaforma digitale. Qualsiasi formato data è accettato, ma Adobe consiglia `YYYY-MM-DD` per coerenza. Utilizza insieme alla [prima data di messa in onda](/help/implementation/variables/standard-metadata/first-air-date.md) per confrontare gli intervalli di rilascio digitali con la trasmissione originale.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.digitalDate` |
| **Campo raccolta XDM** | [`mediaCollection.sessionDetails.firstDigitalDate`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obbligatorio** | No |
| **Inviato con** | Avvio della sessione, chiusura della sessione |

## Web SDK

Imposta `firstDigitalDate` all&#39;interno di `mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        firstDigitalDate: "2016-01-25"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Passa la prima data digitale come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Cotlino)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilizza `createMediaSession` per impostare `firstDigitalDate` in `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "firstDigitalDate": "2016-01-25"
            },
            "playhead": 0
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `firstDigitalDate` in `mediaCollection.sessionDetails`:

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
          "firstDigitalDate": "2016-01-25"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Passa la prima data digitale nell&#39;oggetto `contextData` utilizzando `ADB.Media.VideoMetadataKeys.FirstDigitalDate`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.FirstDigitalDate] = "2016-01-25";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Includi `media.firstDigitalDate` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.firstDigitalDate": "2016-01-25"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).
