---
title: Interruzione annuncio completata
description: Segnala il completamento di tutti gli annunci in un’interruzione pubblicitaria.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 2%

---


# Interruzione annuncio completata

L’evento di completamento dell’interruzione pubblicitaria segnala che tutti gli annunci in un’interruzione pubblicitaria sono stati completati (completati o saltati). Chiude l&#39;interruzione pubblicitaria aperta da [Inizio interruzione pubblicitaria](ad-break-start.md).

* **Prerequisiti**: [Inizio sessione](../session/session-start.md), [Inizio interruzione annuncio](ad-break-start.md)
* **Metrica associata**: nessuna

>[!IMPORTANT]
>
>Ogni `adBreakStart` deve avere un `adBreakComplete` corrispondente. Senza il bookend di chiusura, gli eventi pubblicitari vengono ignorati e la durata dell’annuncio viene attribuita al contenuto principale.

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Chiamare `trackEvent` con il tipo di evento `AdBreakComplete`.

```swift
tracker.trackEvent(event: MediaEvent.AdBreakComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Chiamare `trackEvent` con il tipo di evento `AdBreakComplete`.

```kotlin
tracker.trackEvent(Media.Event.AdBreakComplete, null, null)
```

>[!TAB Roku]

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

>[!TAB API Media Edge]

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

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Chiamare `trackEvent` con il tipo di evento `AdBreakComplete`:

```javascript
tracker.trackEvent(ADB.Media.Event.AdBreakComplete, null, null);
```

>[!TAB Chromecast]

Chiamare `trackEvent` con il tipo di evento `AdBreakComplete`:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete);
```

>[!TAB API Media Collection]

Invia un POST `adBreakComplete` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakComplete"
}
```

>[!ENDTABS]
