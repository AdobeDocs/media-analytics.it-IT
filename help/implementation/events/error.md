---
title: Errore
description: Segnala che il lettore multimediale ha riscontrato un errore.
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
source-wordcount: '193'
ht-degree: 3%
---

# Errore

L’evento di errore segnala che il lettore multimediale ha riscontrato un errore. Il tracciamento di un errore non chiude la sessione. Se l&#39;errore impedisce il proseguimento della riproduzione, chiamare [Session end](session/session-end.md) dopo l&#39;evento di errore.

* **Prerequisiti**: [Inizio sessione](session/session-start.md)
* **Metrica associata**: [[!UICONTROL Error impacted streams]](/help/reporting/metrics/error-impacted-streams.md)

La proprietà `errorDetails.source` accetta solo due valori: `player` (errori originati nel lettore multimediale) e `external` (errori provenienti da un&#39;origine esterna, ad esempio una rete o una rete CDN).

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.error"` e il `errorDetails` richiesto:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.error",
    mediaCollection: {
      errorDetails: {
        name: "media-error-001",
        source: "player"
      },
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

>[!TAB iOS]

Chiamare `trackError` con una stringa ID errore.

```swift
tracker.trackError(errorId: "media-error-001")
```

>[!TAB Android]

Chiamare `trackError` con una stringa ID errore.

```kotlin
tracker.trackError("media-error-001")
```

>[!TAB Edge Roku]

Chiama `sendMediaEvent` con `eventType: "media.error"` e il `errorDetails` richiesto:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.error",
        "mediaCollection": {
            "errorDetails": {
                "name": "media-error-001",
                "source": "player"
            },
            "playhead": 45
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [error](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/error/) con `errorDetails` richiesto:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/error?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.error",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45,
        "errorDetails": {
          "name": "media-error-001",
          "source": "player"
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

Chiamare `trackError` con una stringa ID errore:

```javascript
tracker.trackError("media-error-001");
```

>[!TAB Chromecast]

Chiamare `trackError` con una stringa ID errore:

```javascript
ADBMobile.media.trackError("media-error-001");
```

>[!TAB Roku 2.x]

Chiamare `mediaTrackError` con un ID di errore e l&#39;origine dell&#39;errore. Usa la costante `ERROR_SOURCE_PLAYER` per gli errori del lettore:

```brightscript
adb = ADBMobile()
adb.mediaTrackError("media-error-001", adb.ERROR_SOURCE_PLAYER)
```

>[!TAB API Media Collection]

Invia un POST `error` all&#39;endpoint [eventi](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "error",
  "params": {
    "media.errorId": "media-error-001",
    "media.errorSource": "player"
  }
}
```

>[!ENDTABS]
