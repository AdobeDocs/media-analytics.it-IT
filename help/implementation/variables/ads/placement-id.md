---
title: ID posizionamento
description: Imposta l’ID di posizionamento per ogni annuncio per abilitare le suddivisioni in base al posizionamento dell’annuncio.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 5%

---


# ID posizionamento

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **ID posizionamento**. Vedi [ID posizionamento](/help/reporting/dimensions/placement-id.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile ID posizionamento identifica il posizionamento dell’annuncio (in genere uno slot o una zona definita nella piattaforma ad-server).

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.ad.placement` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.advertisingDetails.placementID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.ad.placement` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio annuncio](/help/implementation/events/ads/ad-start.md), chiusura annuncio |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `placementID` all&#39;interno di `xdm.mediaCollection.advertisingDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        placementID: "placement-12"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passa l’ID di posizionamento come chiave di metadati nell’argomento HashMap a `trackEvent(AdStart)`. Usa `MediaConstants.AdMetadataKeys.PLACEMENT_ID`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.PLACEMENT_ID] = "placement-12"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

Passa l’ID di posizionamento come chiave di metadati nell’argomento HashMap a `trackEvent(AdStart)`. Usa `MediaConstants.AdMetadataKeys.PLACEMENT_ID`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.PLACEMENT_ID] = "placement-12"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku]

Imposta `placementID` in `xdm.mediaCollection.advertisingDetails` quando chiama `sendMediaEvent` per `media.adStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "placementID": "placement-12"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) con `placementID` in `xdm.mediaCollection.advertisingDetails`:

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
          "placementID": "placement-12"
        },
        "sessionID": "{sid}",
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

Passa l&#39;ID di posizionamento nell&#39;oggetto `contextData` utilizzando `ADB.Media.AdMetadataKeys.PlacementId`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.PlacementId] = "placement-12";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

Imposta l&#39;ID posizionamento utilizzando `ADBMobile.media.AdMetadataKeys.PLACEMENT_ID` nell&#39;oggetto metadati standard dell&#39;annuncio:

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.PLACEMENT_ID] = "placement-12";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB API Media Collection]

Includi `media.ad.placementId` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.placementId": "placement-12"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).

>[!ENDTABS]
