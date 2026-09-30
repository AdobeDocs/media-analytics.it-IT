---
title: Ora di inizio dell’interruzione annuncio
description: Imposta l’ora di inizio (offset) dell’interruzione pubblicitaria all’interno del contenuto, in secondi.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 2%
---

# Ora di inizio dell’interruzione annuncio

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Ora di inizio interruzione annuncio**. Vedi [Posizione pod](/help/reporting/dimensions/pod-position.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile del tempo di inizio dell’interruzione pubblicitaria è lo scostamento dell’interruzione pubblicitaria all’interno del contenuto, misurato in secondi. Per un pre-roll il valore è `0`; per un mid-roll il valore è la posizione della testina di riproduzione in cui inizia l&#39;interruzione.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.ad.podSecond` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.advertisingPodDetails.offset`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.ad.podSecond` |
| **Obbligatorio** | Sì |
| **Inviato con** | [Inizio interruzione annuncio](/help/implementation/events/ads/ad-break-start.md), chiusura annuncio |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `offset` all&#39;interno di `xdm.mediaCollection.advertisingPodDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "mid-roll-1",
        index: 2,
        offset: 90
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

Passa il tempo di avvio in secondi come terzo argomento a `createAdBreakObject`.

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "mid-roll-1",
                                              position: 2,
                                             startTime: 90)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

Passa il tempo di avvio in secondi come terzo argomento a `createAdBreakObject`.

```kotlin
val adBreakObject = Media.createAdBreakObject("mid-roll-1",
                                              2L,
                                              90.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Edge Roku]

Imposta `offset` in `xdm.mediaCollection.advertisingPodDetails` quando chiama `sendMediaEvent` per `media.adBreakStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "mid-roll-1",
                "index": 2,
                "offset": 90
            },
            "playhead": 90
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) con `offset` in `xdm.mediaCollection.advertisingPodDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "index": 2,
          "offset": 90
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Passa l&#39;ora di inizio come terzo argomento a `ADB.Media.createAdBreakObject`:

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB Chromecast]

Passa il tempo di avvio in secondi come terzo argomento a `ADBMobile.media.createAdBreakObject`:

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB Roku 2.x]

Passa il tempo di avvio in secondi come secondo argomento a `adb_media_init_adbreakinfo`. Prendere nota dell&#39;ordine dei parametri Roku: `name, startTime, position`.

```brightscript
adb = ADBMobile()
adBreakInfo = adb_media_init_adbreakinfo("mid-roll-1", 90.0, 2)  ' name, startTime, position

adb.mediaTrackEvent(adb.MEDIA_AD_BREAK_START, adBreakInfo)
```

>[!TAB API Media Collection]

Includi `media.ad.podSecond` nell&#39;oggetto `params` della richiesta POST `adBreakStart`:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podSecond": 90
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events).

>[!ENDTABS]
