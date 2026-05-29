---
title: Annuncio completato
description: Segnala che un singolo annuncio ha terminato la riproduzione.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 2%

---


# Annuncio completato

L’evento di completamento dell’annuncio segnala che un singolo annuncio ha terminato la riproduzione. Invia dopo che l’annuncio è stato riprodotto al completamento. Se il visualizzatore ignora l&#39;annuncio, invia [Ignora annuncio](ad-skip.md).

* **Prerequisiti**: [Inizio sessione](../session/session-start.md), [Inizio interruzione annuncio](ad-break-start.md), [Inizio annuncio](ad-start.md)
* **Metrica associata**: [[!UICONTROL Ad completes]](/help/reporting/metrics/ad-completes.md)

>[!IMPORTANT]
>
>Questo evento deve essere circondato da `adBreakStart` e `adBreakComplete` bookend, anche quando viene riprodotto un singolo annuncio. Senza questi bookend, gli eventi pubblicitari vengono ignorati e la durata dell’annuncio viene conteggiata come durata del contenuto principale.

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.adComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 15
    }
  }
});
```

>[!TAB iOS]

Chiamare `trackEvent` con il tipo di evento `AdComplete`.

```swift
tracker.trackEvent(event: MediaEvent.AdComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Chiamare `trackEvent` con il tipo di evento `AdComplete`.

```kotlin
tracker.trackEvent(Media.Event.AdComplete, null, null)
```

>[!TAB Roku]

Chiama `sendMediaEvent` con `eventType: "media.adComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adComplete",
        "mediaCollection": {
            "playhead": 15
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [adComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adcomplete):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 15
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

Chiamare `trackEvent` con il tipo di evento `AdComplete`:

```javascript
tracker.trackEvent(ADB.Media.Event.AdComplete, null, null);
```

>[!TAB Chromecast]

Chiamare `trackEvent` con il tipo di evento `AdComplete`:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete);
```

>[!TAB API Media Collection]

Invia un POST `adComplete` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 15, "ts": 1699523820000 },
  "eventType": "adComplete"
}
```

>[!ENDTABS]
