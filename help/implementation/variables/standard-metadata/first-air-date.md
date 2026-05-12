---
title: Data della prima messa in onda
description: Imposta la data in cui il contenuto è andato in onda per la prima volta in televisione. Adobe consiglia il formato AAAA-MM-GG.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 9%

---


# Data della prima messa in onda

>[!BEGINSHADEBOX]

*In questa pagina sono illustrate le informazioni sulla raccolta dati per la variabile **First air date**. Consulta [Data prima messa in onda](/help/reporting/dimensions/first-air-date.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La prima variabile di data di trasmissione è la data in cui il contenuto è andato in onda per la prima volta in televisione. Qualsiasi formato data è accettato, ma Adobe consiglia `YYYY-MM-DD` per coerenza. Utilizzala per confrontare il coinvolgimento su nuove versioni rispetto al contenuto del catalogo.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.airDate` |
| **Campo raccolta XDM** | [`mediaCollection.sessionDetails.firstAirDate`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obbligatorio** | No |
| **Inviato con** | Avvio della sessione, chiusura della sessione |

## Web SDK

Imposta `firstAirDate` all&#39;interno di `mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        firstAirDate: "2016-01-25"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Passa la prima data di trasmissione come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE] = "2016-01-25"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Cotlino)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE] = "2016-01-25"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilizza `createMediaSession` per impostare `firstAirDate` in `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "firstAirDate": "2016-01-25"
            },
            "playhead": 0
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `firstAirDate` in `mediaCollection.sessionDetails`:

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
          "firstAirDate": "2016-01-25"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Passa la prima data di trasmissione nell&#39;oggetto `contextData` utilizzando `ADB.Media.VideoMetadataKeys.FirstAirDate`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.FirstAirDate] = "2016-01-25";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Includi `media.firstAirDate` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.firstAirDate": "2016-01-25"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).
