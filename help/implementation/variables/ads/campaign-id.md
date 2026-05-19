---
title: ID campagna
description: Imposta l’identificatore della campagna per ogni annuncio in modo che il coinvolgimento possa essere aggregato per campagna.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 8%

---


# ID campagna

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **ID campagna**. Vedi [ID campagna](/help/reporting/dimensions/campaign-id.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile ID campagna identifica la campagna pubblicitaria a cui appartiene il contenuto creativo. Qualsiasi valore stringa (in genere un ID campagna dalla piattaforma ad-server) è accettabile. Utilizza la variabile per aggregare il coinvolgimento tra più creatività che condividono una campagna.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.ad.campaign` |
| **Campo raccolta XDM** | [`mediaCollection.advertisingDetails.campaignID`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.ad.campaign` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio annuncio](/help/implementation/events/ads/ad-start.md), chiusura annuncio |

## Web SDK

Imposta `campaignID` all&#39;interno di `mediaCollection.advertisingDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        campaignID: "fall-2024"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

Passa l&#39;ID campagna come chiave di metadati nell&#39;argomento HashMap a `trackEvent(AdStart)`. Usa `MediaConstants.AdMetadataKeys.CAMPAIGN_ID`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Cotlino)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

Imposta `campaignID` in `mediaCollection.advertisingDetails` quando chiama `sendMediaEvent` per `media.adStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "campaignID": "fall-2024"
            },
            "playhead": 0
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) con `campaignID` in `mediaCollection.advertisingDetails`:

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
          "campaignID": "fall-2024"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Passa l&#39;ID della campagna nell&#39;oggetto `contextData` utilizzando `ADB.Media.AdMetadataKeys.CampaignId`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CampaignId] = "fall-2024";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## API Media Collection

Includi `media.ad.campaignId` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.campaignId": "fall-2024"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).
