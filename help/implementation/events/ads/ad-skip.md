---
title: Salta annuncio
description: Segnala che il visualizzatore ha saltato un annuncio.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 2%

---


# Salta annuncio

L’evento di salto dell’annuncio segnala che il visualizzatore ha saltato un annuncio prima del suo completamento. Invialo quando il visualizzatore seleziona il pulsante Ignora. Invia [Annuncio completato](ad-complete.md) se l&#39;annuncio viene riprodotto fino al completamento.

* **Prerequisiti**: [Inizio sessione](../session/session-start.md), [Inizio interruzione annuncio](ad-break-start.md), [Inizio annuncio](ad-start.md)
* **Metrica associata**: nessuna

>[!IMPORTANT]
>
>Questo evento deve essere circondato da `adBreakStart` e `adBreakComplete` bookend, anche quando viene riprodotto un singolo annuncio. Senza questi bookend, gli eventi pubblicitari vengono ignorati e la durata dell’annuncio viene conteggiata come durata del contenuto principale.

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.adSkip"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 5
    }
  }
});
```

>[!TAB iOS]

Chiamare `trackEvent` con il tipo di evento `AdSkip`.

```swift
tracker.trackEvent(event: MediaEvent.AdSkip, info: nil, metadata: nil)
```

>[!TAB Android]

Chiamare `trackEvent` con il tipo di evento `AdSkip`.

```kotlin
tracker.trackEvent(Media.Event.AdSkip, null, null)
```

>[!TAB Edge Roku]

Chiama `sendMediaEvent` con `eventType: "media.adSkip"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adSkip",
        "mediaCollection": {
            "playhead": 5
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [adSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adskip):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 5
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

Chiamare `trackEvent` con il tipo di evento `AdSkip`:

```javascript
tracker.trackEvent(ADB.Media.Event.AdSkip, null, null);
```

>[!TAB Chromecast]

Chiamare `trackEvent` con il tipo di evento `AdSkip`:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdSkip);
```

>[!TAB Roku 2.x]

Chiamare `mediaTrackEvent` con il tipo di evento `MEDIA_AD_SKIP`:

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_AD_SKIP)
```

>[!TAB API Media Collection]

Invia un POST `adSkip` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 5, "ts": 1699523820000 },
  "eventType": "adSkip"
}
```

>[!ENDTABS]
