---
title: Inizio annuncio
description: Segnala l’inizio della riproduzione di un singolo annuncio.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---


# Inizio annuncio

L’evento di inizio annuncio segnala l’inizio della riproduzione di un singolo annuncio. Deve verificarsi all&#39;interno di una coppia [Inizio interruzione annuncio](ad-break-start.md) / [Interruzione annuncio completata](ad-break-complete.md).

* **Prerequisiti**: [Inizio sessione](../session/session-start.md), [Inizio interruzione annuncio](ad-break-start.md)
* **Metrica associata**: [[!UICONTROL Ad starts]](/help/reporting/metrics/ad-starts.md)

>[!IMPORTANT]
>
>Questo evento deve essere circondato da `adBreakStart` e `adBreakComplete` bookend, anche quando viene riprodotto un singolo annuncio. Senza questi bookend, gli eventi pubblicitari vengono ignorati e la durata dell’annuncio viene conteggiata come durata del contenuto principale.

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.adStart"` e il `advertisingDetails` richiesto:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        friendlyName: "Ford F-150",
        length: 15,
        playerName: "Freewheel",
        podPosition: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passa il nome, l&#39;ID, la posizione e la lunghezza dell&#39;annuncio a `createAdObject`, quindi chiama `trackEvent`.

```swift
let adObject = Media.createAdObjectWith(name: "Ford F-150",
                                          id: "ad-2125",
                                    position: 0,
                                      length: 15)

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: nil)
```

>[!TAB Android]

Passa il nome, l&#39;ID, la posizione e la lunghezza dell&#39;annuncio a `createAdObject`, quindi chiama `trackEvent`.

```kotlin
val adObject = Media.createAdObject("Ford F-150",
                                    "ad-2125",
                                    0,
                                    15)

tracker.trackEvent(Media.Event.AdStart, adObject, null)
```

>[!TAB Edge Roku]

Chiama `sendMediaEvent` con `eventType: "media.adStart"` e il `advertisingDetails` richiesto:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "friendlyName": "Ford F-150",
                "length": 15,
                "playerName": "Roku Player",
                "podPosition": 0
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) con `advertisingDetails` richiesto:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0
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

Passa il nome, l&#39;ID, la posizione e la lunghezza dell&#39;annuncio a `ADB.Media.createAdObject`:

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",  // name (friendly name)
  "ad-2125",     // ad ID
  0,             // position in pod
  15             // length (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, null);
```

>[!TAB Chromecast]

Passa il nome, l&#39;ID, la posizione e la lunghezza dell&#39;annuncio a `ADBMobile.media.createAdObject`:

```javascript
var adInfo = ADBMobile.media.createAdObject(
  "Ford F-150",  // name (friendly name)
  "ad-2125",     // ad ID
  0,             // position in pod
  15             // length (seconds)
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

Crea un oggetto annuncio con `adb_media_init_adinfo`, quindi tieni traccia dell&#39;evento. La posizione dell’annuncio all’interno del pod è basata su 1.

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 15.0)  ' name, id, position, length

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB API Media Collection]

Invia un POST `adStart` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "ad-2125",
    "media.ad.name": "Ford F-150",
    "media.ad.length": 15,
    "media.ad.podPosition": 0
  }
}
```

>[!ENDTABS]
