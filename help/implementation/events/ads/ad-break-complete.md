---
title: Interruzione annuncio completata
description: Segnala il completamento di tutti gli annunci in un’interruzione pubblicitaria.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 6%

---


# Interruzione annuncio completata

L’evento di completamento dell’interruzione pubblicitaria segnala che tutti gli annunci in un’interruzione pubblicitaria sono stati completati (completati o saltati). Chiude l&#39;interruzione pubblicitaria aperta da [Inizio interruzione pubblicitaria](ad-break-start.md).

* **Prerequisiti**: [Inizio sessione](../session/session-start.md), [Inizio interruzione annuncio](ad-break-start.md)
* **Metrica associata**: nessuna

>[!IMPORTANT]
>
>Ogni `adBreakStart` deve avere un `adBreakComplete` corrispondente. Senza il bookend di chiusura, gli eventi pubblicitari vengono ignorati e la durata dell’annuncio viene attribuita al contenuto principale.

## Web SDK

Chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.adBreakComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

Chiamare `trackEvent` con il tipo di evento `AdBreakComplete`.

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.AdBreakComplete, info: nil, metadata: nil)
```

**Android (Cotlino)**

```kotlin
tracker.trackEvent(Media.Event.AdBreakComplete, null, null)
```

## Roku (BrightScript)

Chiama `sendMediaEvent` con `eventType: "media.adBreakComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakComplete",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [adBreakComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakcomplete):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

Chiamare `trackEvent` con il tipo di evento `AdBreakComplete`:

```javascript
tracker.trackEvent(ADB.Media.Event.AdBreakComplete, null, null);
```

## API Media Collection

Invia un POST `adBreakComplete` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakComplete"
}
```
