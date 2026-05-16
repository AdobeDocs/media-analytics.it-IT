---
title: Nome interruzione annuncio
description: Imposta il nome descrittivo dell’interruzione pubblicitaria principale.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 5%

---


# Nome interruzione annuncio

>[!BEGINSHADEBOX]

*In questa pagina sono illustrate le informazioni sulla raccolta dati per la variabile **Ad Break Name**. Vedi [Nome pod](/help/reporting/dimensions/pod-name.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile del nome dell’interruzione pubblicitaria è il nome descrittivo dell’interruzione pubblicitaria (ad esempio, `"pre-roll"`, `"mid-roll-1"`, `"post-roll"`). Il valore viene impostato sull’oggetto interruzione pubblicitaria, non sui singoli annunci.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.ad.podFriendlyName` |
| **Campo raccolta XDM** | [`mediaCollection.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.ad.podFriendlyName` |
| **Obbligatorio** | Sì (Mobile SDK); No (Edge, Media Collection API) |
| **Inviato con** | [Inizio interruzione annuncio](/help/implementation/events/ads/ad-break-start.md), chiusura annuncio |

## Web SDK

Imposta `friendlyName` in `mediaCollection.advertisingPodDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview) per `media.adBreakStart`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "pre-roll",
        index: 1,
        offset: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

Passa il nome dell&#39;interruzione pubblicitaria come primo argomento (`name`) a `createAdBreakObject`, quindi tieni traccia dell&#39;evento di avvio dell&#39;annuncio prima dell&#39;evento di inizio annuncio.

**iOS (Swift)**

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

**Android (Cotlino)**

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1L,
                                              0.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku (BrightScript)

Imposta `friendlyName` in `mediaCollection.advertisingPodDetails` quando chiama `sendMediaEvent` per `media.adBreakStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "pre-roll",
                "index": 1,
                "offset": 0
            },
            "playhead": 0
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) con `friendlyName` in `mediaCollection.advertisingPodDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "friendlyName": "pre-roll",
          "index": 1,
          "offset": 0
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Passa il nome dell&#39;interruzione pubblicitaria come primo argomento a `ADB.Media.createAdBreakObject`:

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",
  1,
  0
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## API Media Collection

Includi `media.ad.podFriendlyName` nell&#39;oggetto `params` della richiesta POST `adBreakStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podFriendlyName": "pre-roll"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).
