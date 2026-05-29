---
title: Nome del lettore dell’annuncio
description: Imposta il nome del lettore che genera gli annunci. Il lettore dell’annuncio può differire dal lettore del contenuto principale.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 2%

---


# Nome del lettore dell’annuncio

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Ad Player name**. Vedi [Nome del lettore dell&#39;annuncio](/help/reporting/dimensions/ad-player-name.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile del nome del lettore dell&#39;annuncio identifica quale lettore ha eseguito il rendering di ciascun annuncio (ad esempio, `"Freewheel"`, `"Google IMA"`). Il lettore di annunci può differire dal lettore di contenuto principale quando gli annunci sono uniti da un servizio di inserimento di annunci lato server. Utilizza questa variabile per confrontare qualità e completamento tra gli stack di ad-serving.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.ad.playerName` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.advertisingDetails.playerName`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.ad.playerName` |
| **Obbligatorio** | Sì |
| **Inviato con** | [Inizio annuncio](/help/implementation/events/ads/ad-start.md), chiusura annuncio |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `playerName` all&#39;interno di `xdm.mediaCollection.advertisingDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        playerName: "Freewheel"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passa il nome del lettore dell&#39;annuncio come chiave `MediaConstants.AdMetadataKeys.AD_PLAYER` nell&#39;argomento HashMap dei metadati a `trackEvent(AdStart)`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

Passa il nome del lettore dell&#39;annuncio come chiave `MediaConstants.AdMetadataKeys.AD_PLAYER` nell&#39;argomento HashMap dei metadati a `trackEvent(AdStart)`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku]

Imposta `playerName` in `xdm.mediaCollection.advertisingDetails` quando chiama `sendMediaEvent` per `media.adStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "playerName": "Freewheel",
                "length": 15,
                "podPosition": 0
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) con `playerName` in `xdm.mediaCollection.advertisingDetails`:

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
          "podPosition": 0
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

Passa il nome del lettore dell&#39;annuncio nell&#39;oggetto `contextData` utilizzando `ADB.Media.AdMetadataKeys.AdPlayer`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.AdPlayer] = "Freewheel";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

Passa il nome del lettore dell’annuncio nell’oggetto metadati contestuali durante il tracciamento dell’evento di inizio annuncio:

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var metadata = { "a.media.ad.playerName": "Chromecast Player" };
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, metadata);
```

>[!TAB API Media Collection]

Includi `media.ad.playerName` nell&#39;oggetto `params` della richiesta POST `adStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.playerName": "Freewheel"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).

>[!ENDTABS]
