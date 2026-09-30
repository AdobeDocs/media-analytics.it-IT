---
title: Play
description: Segnala che il lettore multimediale è entrato nello stato di riproduzione.
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
source-wordcount: '185'
ht-degree: 3%
---

# Play

L’evento di riproduzione segnala che il lettore multimediale ha cambiato stato in riproduzione. Invialo all’inizio iniziale del contenuto, alla riproduzione automatica e ogni volta che il lettore riprende dopo una pausa o un buffer. Non esiste un evento di ripresa separato; un evento di riproduzione dopo [Pausa avvio](pause-start.md) o [Avvio buffer](buffer-start.md) funge da ripresa.

* **Prerequisiti**: [Inizio sessione](../session/session-start.md)
* **Metrica associata**: [[!UICONTROL Content starts]](/help/reporting/metrics/content-starts.md)

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.play"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.play",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Chiamare `trackPlay` quando il lettore multimediale inizia o riprende la riproduzione.

```swift
tracker.trackPlay()
```

>[!TAB Android]

Chiamare `trackPlay` quando il lettore multimediale inizia o riprende la riproduzione.

```kotlin
tracker.trackPlay()
```

>[!TAB Edge Roku]

Chiama `sendMediaEvent` con `eventType: "media.play"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [play](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/play/):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/play?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.play",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
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

Chiamare `trackPlay` quando il lettore multimediale inizia o riprende la riproduzione:

```javascript
tracker.trackPlay();
```

>[!TAB Chromecast]

Chiamare `trackPlay` quando il lettore multimediale inizia o riprende la riproduzione:

```javascript
ADBMobile.media.trackPlay();
```

>[!TAB Roku 2.x]

Chiamare `mediaTrackPlay` quando il lettore multimediale inizia o riprende la riproduzione:

```brightscript
ADBMobile().mediaTrackPlay()
```

>[!TAB API Media Collection]

Invia un POST `play` all&#39;endpoint [eventi](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "play"
}
```

>[!ENDTABS]
