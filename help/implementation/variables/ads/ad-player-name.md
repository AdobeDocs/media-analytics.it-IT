---
title: Nome del lettore dell’annuncio
description: Imposta il nome del lettore che genera gli annunci. Il lettore dell’annuncio può differire dal lettore del contenuto principale.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 5%

---


# Nome del lettore dell’annuncio

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Ad Player name**. Vedi [Nome del lettore dell&#39;annuncio](/help/reporting/dimensions/ad-player-name.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile del nome del lettore dell&#39;annuncio identifica quale lettore ha eseguito il rendering di ciascun annuncio (ad esempio, `"Freewheel"`, `"Google IMA"`). Il lettore di annunci può differire dal lettore di contenuto principale quando gli annunci sono uniti da un servizio di inserimento di annunci lato server. Utilizza questa variabile per confrontare qualità e completamento tra gli stack di ad-serving.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.ad.playerName` |
| **Campo raccolta XDM** | [`mediaCollection.advertisingDetails.playerName`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Obbligatorio** | Sì |
| **Inviato con** | Avvio annuncio, chiusura annuncio |

## Web SDK

Imposta `playerName` all&#39;interno di `mediaCollection.advertisingDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

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

## Mobile SDK

Passa il nome del lettore dell&#39;annuncio come chiave `MediaConstants.AdMetadataKeys.AD_PLAYER` nell&#39;argomento HashMap dei metadati a `trackEvent(AdStart)`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Cotlino)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

Imposta `playerName` in `mediaCollection.advertisingDetails` quando chiama `sendMediaEvent` per `media.adStart`:

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

## API di Media Edge

Chiama l&#39;endpoint [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) con `playerName` in `mediaCollection.advertisingDetails`:

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

## Media SDK

Passa il nome del lettore dell&#39;annuncio nell&#39;oggetto `contextData` utilizzando `ADB.Media.AdMetadataKeys.AdPlayer`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.AdPlayer] = "Freewheel";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## API Media Collection

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
