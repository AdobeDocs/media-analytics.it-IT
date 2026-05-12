---
title: ID sito
description: Imposta l’ID del sito dell’annuncio per ogni annuncio per abilitare le suddivisioni per sito di posizionamento dell’annuncio.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 8%

---


# ID sito

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **ID sito**. Vedi [ID sito](/help/reporting/dimensions/site-id.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile ID sito identifica il sito dell’annuncio. Qualsiasi valore stringa (in genere un ID dalla piattaforma ad-server) è accettabile.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.ad.site` |
| **Campo raccolta XDM** | [`mediaCollection.advertisingDetails.siteID`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Obbligatorio** | No |
| **Inviato con** | Avvio annuncio, chiusura annuncio |

## Web SDK

Imposta `siteID` all&#39;interno di `mediaCollection.advertisingDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        siteID: "site-42"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

Passa l&#39;ID sito come chiave di metadati nell&#39;argomento HashMap a `trackEvent(AdStart)`. Usa `MediaConstants.AdMetadataKeys.SITE_ID`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.SITE_ID] = "site-42"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Cotlino)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.SITE_ID] = "site-42"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

Imposta `siteID` in `mediaCollection.advertisingDetails` quando chiama `sendMediaEvent` per `media.adStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "siteID": "site-42"
            },
            "playhead": 0
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) con `siteID` in `mediaCollection.advertisingDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0,
          "siteID": "site-42"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Passa l&#39;ID sito nell&#39;oggetto `contextData` utilizzando `ADB.Media.AdMetadataKeys.SiteId`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.SiteId] = "site-42";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## API Media Collection

Includi `media.ad.siteId` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.siteId": "site-42"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).
