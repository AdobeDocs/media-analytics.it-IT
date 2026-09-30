---
title: Sessione completata
description: Segnala che il visualizzatore ha raggiunto la fine del contenuto principale.
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
source-wordcount: '186'
ht-degree: 2%
---

# Sessione completata

L’evento di completamento della sessione segnala che il visualizzatore ha raggiunto la fine del contenuto principale. Non chiude immediatamente la sessione; la sessione rimane aperta fino alla scadenza naturale. Per chiudere immediatamente la sessione, chiamare [Session end](session-end.md).

* **Prerequisiti**: [Inizio sessione](session-start.md)
* **Metrica associata**: [[!UICONTROL Content completes]](/help/reporting/metrics/content-completes.md)

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.sessionComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 128
    }
  }
});
```

>[!TAB iOS]

Chiamare `trackComplete` quando il lettore multimediale raggiunge la fine del contenuto.

```swift
tracker.trackComplete()
```

>[!TAB Android]

Chiamare `trackComplete` quando il lettore multimediale raggiunge la fine del contenuto.

```kotlin
tracker.trackComplete()
```

>[!TAB Edge Roku]

Chiama `sendMediaEvent` con `eventType: "media.sessionComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
            "playhead": 128
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [sessionComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessioncomplete):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 128
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

Chiamare `trackComplete` quando il lettore multimediale raggiunge la fine del contenuto:

```javascript
tracker.trackComplete();
```

>[!TAB Chromecast]

Chiamare `trackComplete` quando il lettore multimediale raggiunge la fine del contenuto:

```javascript
ADBMobile.media.trackComplete();
```

>[!TAB Roku 2.x]

Chiamare `mediaTrackComplete` quando il lettore multimediale raggiunge la fine del contenuto:

```brightscript
ADBMobile().mediaTrackComplete()
```

>[!TAB API Media Collection]

Invia un POST `sessionComplete` all&#39;endpoint [eventi](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 128, "ts": 1699523820000 },
  "eventType": "sessionComplete"
}
```

>[!ENDTABS]
