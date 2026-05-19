---
title: Errore
description: Segnala che il lettore multimediale ha riscontrato un errore.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 7%

---


# Errore

L’evento di errore segnala che il lettore multimediale ha riscontrato un errore. Il tracciamento di un errore non chiude la sessione. Se l&#39;errore impedisce il proseguimento della riproduzione, chiamare [Session end](session/session-end.md) dopo l&#39;evento di errore.

* **Prerequisiti**: [Inizio sessione](session/session-start.md)
* **Metrica associata**: [Flussi interessati dall&#39;errore](/help/reporting/metrics/error-impacted-streams.md)

La proprietà `errorDetails.source` accetta solo due valori: `player` (errori originati nel lettore multimediale) e `external` (errori provenienti da un&#39;origine esterna, ad esempio una rete o una rete CDN).

## Web SDK

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

## Mobile SDK

Chiamare `trackError` con una stringa ID errore.

**iOS (Swift)**

```swift
tracker.trackError(errorId: "media-error-001")
```

**Android (Cotlino)**

```kotlin
tracker.trackError("media-error-001")
```

## Roku (BrightScript)

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

## API di Media Edge

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

## Media SDK

Chiamare `trackError` con una stringa ID errore:

```javascript
tracker.trackError("media-error-001");
```

## API Media Collection

Invia un POST `error` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

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
