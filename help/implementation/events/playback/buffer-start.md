---
title: Avvio buffer
description: Segnala che il lettore multimediale è entrato in uno stato di buffering.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 6%

---


# Avvio buffer

L’evento di avvio del buffer segnala che il lettore multimediale è entrato in uno stato di buffering.

* **Prerequisiti**: [Inizio sessione](../session/session-start.md)
* **Metrica associata**: [Eventi buffer](/help/reporting/metrics/buffer-events.md)

>[!NOTE]
>
>**API basate su XDM (Web SDK, Roku, Media Edge API, Media Collection API):** non esiste alcun tipo di evento di ripresa del buffer; la fine del buffer viene dedotta quando si invia un evento [`play`](play.md) dopo `bufferStart`.
>
>**Mobile SDK:** Chiama `trackEvent(BufferComplete)` quando il lettore esce dal buffering, quindi chiama `trackPlay()` per riprendere la riproduzione.

## Web SDK

Chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.bufferStart"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bufferStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## Mobile SDK

Chiama `trackEvent` con `BufferStart` quando il lettore entra in uno stato di buffering e `BufferComplete` quando esce.

**iOS (Swift)**

```swift
// Buffer starts
tracker.trackEvent(event: MediaEvent.BufferStart, info: nil, metadata: nil)

// Buffer ends
tracker.trackEvent(event: MediaEvent.BufferComplete, info: nil, metadata: nil)
```

**Android (Cotlino)**

```kotlin
// Buffer starts
tracker.trackEvent(Media.Event.BufferStart, null, null)

// Buffer ends
tracker.trackEvent(Media.Event.BufferComplete, null, null)
```

## Roku (BrightScript)

Chiama `sendMediaEvent` con `eventType: "media.bufferStart"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [bufferStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bufferstart/):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bufferStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bufferStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

Chiamare `trackEvent` con il tipo di evento `BufferStart`:

```javascript
tracker.trackEvent(ADB.Media.Event.BufferStart, null, null);
```

## API Media Collection

Invia un POST `bufferStart` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "bufferStart"
}
```
