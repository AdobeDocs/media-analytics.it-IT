---
title: URL creatività
description: Imposta l’URL della creatività dell’annuncio per ogni annuncio.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 8%

---


# URL creatività

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **URL Creative**. Vedi [URL Creative](/help/reporting/dimensions/creative-url.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile URL creativa è l’URL della creatività dell’annuncio. Utilizza la variabile per tenere traccia della posizione della risorsa di ogni contenuto creativo quando l’URL stesso è significativo per l’analisi (ad esempio, per distinguere i percorsi CDN o le versioni creative).

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.ad.creativeURL` |
| **Campo raccolta XDM** | [`mediaCollection.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Obbligatorio** | No |
| **Inviato con** | Avvio annuncio, chiusura annuncio |

## Web SDK

Imposta `creativeURL` all&#39;interno di `mediaCollection.advertisingDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        creativeURL: "https://cdn.example.com/ads/creative-987.mp4"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

Passa l&#39;URL creativo come chiave di metadati nell&#39;argomento HashMap a `trackEvent(AdStart)`. Usa `MediaConstants.AdMetadataKeys.CREATIVE_URL`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Cotlino)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

Imposta `creativeURL` in `mediaCollection.advertisingDetails` quando chiama `sendMediaEvent` per `media.adStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
            },
            "playhead": 0
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) con `creativeURL` in `mediaCollection.advertisingDetails`:

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
          "creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Passa l&#39;URL creativo nell&#39;oggetto `contextData` utilizzando `ADB.Media.AdMetadataKeys.CreativeUrl`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CreativeUrl] = "https://cdn.example.com/ads/creative-987.mp4";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## API Media Collection

Includi `media.ad.creativeURL` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).
