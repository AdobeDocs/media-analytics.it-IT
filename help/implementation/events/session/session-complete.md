---
title: Sessione completata
description: Segnala che il visualizzatore ha raggiunto la fine del contenuto principale.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 6%

---


# Sessione completata

L’evento di completamento della sessione segnala che il visualizzatore ha raggiunto la fine del contenuto principale. Non chiude immediatamente la sessione; la sessione rimane aperta fino alla scadenza naturale. Per chiudere immediatamente la sessione, chiamare [Session end](session-end.md).

* **Prerequisiti**: [Inizio sessione](session-start.md)
* **Metrica associata**: [Completamento contenuto](/help/reporting/metrics/content-completes.md)

## Web SDK

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

## Mobile SDK

Chiamare `trackComplete` quando il lettore multimediale raggiunge la fine del contenuto.

**iOS (Swift)**

```swift
tracker.trackComplete()
```

**Android (Cotlino)**

```kotlin
tracker.trackComplete()
```

## Roku (BrightScript)

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

## API di Media Edge

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

## Media SDK

Chiamare `trackComplete` quando il lettore multimediale raggiunge la fine del contenuto:

```javascript
tracker.trackComplete();
```

## API Media Collection

Invia un POST `sessionComplete` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 128, "ts": 1699523820000 },
  "eventType": "sessionComplete"
}
```
