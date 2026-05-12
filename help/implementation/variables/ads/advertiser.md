---
title: Inserzionista
description: Imposta l’azienda o il brand presente in ogni annuncio.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 8%

---


# Inserzionista

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Advertiser**. Vedi [Inserzionista](/help/reporting/dimensions/advertiser.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile dell&#39;inserzionista è l&#39;azienda o il brand visualizzato nell&#39;annuncio (ad esempio, `"Ford"` o `"Coca-Cola"`). Utilizza la variabile per interrompere il coinvolgimento e il completamento da parte dell’inserzionista.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.ad.advertiser` |
| **Campo raccolta XDM** | [`mediaCollection.advertisingDetails.advertiser`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Obbligatorio** | No |
| **Inviato con** | Avvio annuncio, chiusura annuncio |

## Web SDK

Imposta `advertiser` all&#39;interno di `mediaCollection.advertisingDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        advertiser: "Ford"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

Passa l&#39;inserzionista come chiave di metadati nell&#39;argomento HashMap a `trackEvent(AdStart)`. Usa `MediaConstants.AdMetadataKeys.ADVERTISER`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.ADVERTISER] = "Ford"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Cotlino)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.ADVERTISER] = "Ford"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

Imposta `advertiser` in `mediaCollection.advertisingDetails` quando chiama `sendMediaEvent` per `media.adStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "advertiser": "Ford"
            },
            "playhead": 0
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) con `advertiser` in `mediaCollection.advertisingDetails`:

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
          "advertiser": "Ford"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Passa l&#39;inserzionista nell&#39;oggetto `contextData` utilizzando `ADB.Media.AdMetadataKeys.Advertiser`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.Advertiser] = "Ford";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## API Media Collection

Includi `media.ad.advertiser` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.advertiser": "Ford"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).
