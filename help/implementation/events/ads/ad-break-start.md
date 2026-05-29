---
title: Avvio dell’interruzione pubblicitaria
description: Segnala l’inizio di un’interruzione pubblicitaria (una sequenza di uno o più annunci).
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 1%

---


# Avvio dell’interruzione pubblicitaria

L’evento di inizio dell’interruzione pubblicitaria segnala l’inizio di un’interruzione pubblicitaria. Un’interruzione pubblicitaria è una sequenza di uno o più annunci. Ogni evento `adStart`, `adComplete` e `adSkip` deve verificarsi tra una coppia `adBreakStart` e `adBreakComplete`, anche quando viene riprodotto un singolo annuncio.

* **Prerequisiti**: [Inizio sessione](../session/session-start.md)
* **Metrica associata**: nessuna

>[!IMPORTANT]
>
>Gli eventi annuncio (`adStart`, `adComplete`, `adSkip`) vengono ignorati senza `adBreakStart` e `adBreakComplete` bookend. Senza di essi, la durata dell’annuncio viene attribuita alla durata del contenuto principale, che influisce sui dati di reporting aggregati.

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.adBreakStart"` e il `advertisingPodDetails` richiesto:

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

>[!TAB iOS]

Passa il nome, la posizione e l&#39;ora di inizio dell&#39;interruzione pubblicitaria a `createAdBreakObject`, quindi chiama `trackEvent`.

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

Passa il nome, la posizione e l&#39;ora di inizio dell&#39;interruzione pubblicitaria a `createAdBreakObject`, quindi chiama `trackEvent`.

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1,
                                              0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Roku]

Chiama `sendMediaEvent` con `eventType: "media.adBreakStart"` e il `advertisingPodDetails` richiesto:

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

>[!TAB API Media Edge]

Chiama l&#39;endpoint [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) con `advertisingPodDetails` richiesto:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "advertisingPodDetails": {
          "index": 0,
          "offset": 0
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Passa il nome, la posizione e l&#39;ora di inizio dell&#39;interruzione pubblicitaria a `ADB.Media.createAdBreakObject`:

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",  // name
  1,           // position
  0            // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB Chromecast]

Passa il nome, la posizione e l&#39;ora di inizio dell&#39;interruzione pubblicitaria a `ADBMobile.media.createAdBreakObject`:

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "pre-roll",  // name
  1,           // position
  0            // start time (seconds)
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB API Media Collection]

Invia un POST `adBreakStart` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podFriendlyName": "pre-roll",
    "media.ad.podIndex": 1,
    "media.ad.podSecond": 0
  }
}
```

>[!ENDTABS]
