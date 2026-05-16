---
title: Play
description: Segnala che il lettore multimediale è entrato nello stato di riproduzione.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 7%

---


# Play

L’evento di riproduzione segnala che il lettore multimediale ha cambiato stato in riproduzione. Invialo all’inizio iniziale del contenuto, alla riproduzione automatica e ogni volta che il lettore riprende dopo una pausa o un buffer. Non esiste un evento di ripresa separato; un evento di riproduzione dopo [Pausa avvio](pause-start.md) o [Avvio buffer](buffer-start.md) funge da ripresa.

* **Prerequisiti**: [Inizio sessione](../session/session-start.md)
* **Metrica associata**: [Inizio contenuto](/help/reporting/metrics/content-starts.md)

## Web SDK

Chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.play"`:

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

## Mobile SDK

Chiamare `trackPlay` quando il lettore multimediale inizia o riprende la riproduzione.

**iOS (Swift)**

```swift
tracker.trackPlay()
```

**Android (Cotlino)**

```kotlin
tracker.trackPlay()
```

## Roku (BrightScript)

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

## API di Media Edge

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

## Media SDK

Chiamare `trackPlay` quando il lettore multimediale inizia o riprende la riproduzione:

```javascript
tracker.trackPlay();
```

## API Media Collection

Invia un POST `play` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "play"
}
```
