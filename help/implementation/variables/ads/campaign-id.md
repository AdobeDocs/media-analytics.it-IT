---
title: ID campagna
description: Imposta l’identificatore della campagna per ogni annuncio in modo che il coinvolgimento possa essere aggregato per campagna.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 4%

---


# ID campagna

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **ID campagna**. Vedi [ID campagna](/help/reporting/dimensions/campaign-id.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile ID campagna identifica la campagna pubblicitaria a cui appartiene il contenuto creativo. Qualsiasi valore stringa (in genere un ID campagna dalla piattaforma ad-server) è accettabile. Utilizza la variabile per aggregare il coinvolgimento tra più creatività che condividono una campagna.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.ad.campaign` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.advertisingDetails.campaignID`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.ad.campaign` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio annuncio](/help/implementation/events/ads/ad-start.md), chiusura annuncio |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `campaignID` all&#39;interno di `xdm.mediaCollection.advertisingDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

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

>[!TAB iOS]

Passa l&#39;ID campagna come chiave di metadati nell&#39;argomento HashMap a `trackEvent(AdStart)`. Usa `MediaConstants.AdMetadataKeys.CAMPAIGN_ID`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

Passa l&#39;ID campagna come chiave di metadati nell&#39;argomento HashMap a `trackEvent(AdStart)`. Usa `MediaConstants.AdMetadataKeys.CAMPAIGN_ID`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Edge Roku]

Imposta `campaignID` in `xdm.mediaCollection.advertisingDetails` quando chiama `sendMediaEvent` per `media.adStart`:

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

>[!TAB API Media Edge]

Chiama l&#39;endpoint [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) con `campaignID` in `xdm.mediaCollection.advertisingDetails`:

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

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Passa l&#39;ID della campagna nell&#39;oggetto `contextData` utilizzando `ADB.Media.AdMetadataKeys.CampaignId`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CampaignId] = "fall-2024";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

Imposta l&#39;ID campagna utilizzando `ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID` nell&#39;oggetto metadati standard dell&#39;annuncio:

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

Imposta l&#39;ID campagna utilizzando `MEDIA_AdMetadataKeyCAMPAIGN_ID` nell&#39;oggetto metadati standard dell&#39;annuncio:

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)

standardAdMetadata = {}
standardAdMetadata[adb.MEDIA_AdMetadataKeyCAMPAIGN_ID] = "fall-2024"
adInfo[adb.MEDIA_STANDARD_AD_METADATA] = standardAdMetadata

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB API Media Collection]

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

>[!ENDTABS]
