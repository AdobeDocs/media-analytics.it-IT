---
title: Avvio buffer
description: Segnala che il lettore multimediale è entrato in uno stato di buffering.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 2%

---


# Avvio buffer

L’evento di avvio del buffer segnala che il lettore multimediale è entrato in uno stato di buffering.

* **Prerequisiti**: [Inizio sessione](../session/session-start.md)
* **Metrica associata**: [[!UICONTROL Buffer events]](/help/reporting/metrics/buffer-events.md)

>[!NOTE]
>
>**API basate su XDM (Web SDK, Roku, Media Edge API, Media Collection API):** non esiste alcun tipo di evento di ripresa del buffer; la fine del buffer viene dedotta quando si invia un evento [`play`](play.md) dopo `bufferStart`.
>
>**Mobile SDK:** Chiama `trackEvent(BufferComplete)` quando il lettore esce dal buffering, quindi chiama `trackPlay()` per riprendere la riproduzione.

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Chiama `trackEvent` con `BufferStart` quando il lettore entra in uno stato di buffering e `BufferComplete` quando esce.

```swift
// Buffer starts
tracker.trackEvent(event: MediaEvent.BufferStart, info: nil, metadata: nil)

// Buffer ends
tracker.trackEvent(event: MediaEvent.BufferComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Chiama `trackEvent` con `BufferStart` quando il lettore entra in uno stato di buffering e `BufferComplete` quando esce.

```kotlin
// Buffer starts
tracker.trackEvent(Media.Event.BufferStart, null, null)

// Buffer ends
tracker.trackEvent(Media.Event.BufferComplete, null, null)
```

>[!TAB Edge Roku]

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

>[!TAB API Media Edge]

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

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Chiamare `trackEvent` con il tipo di evento `BufferStart`:

```javascript
tracker.trackEvent(ADB.Media.Event.BufferStart, null, null);
```

>[!TAB Chromecast]

Chiama `trackEvent` con `BufferStart` quando il lettore entra in uno stato di buffering e `BufferComplete` quando esce:

```javascript
// Buffer starts
ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);

// Buffer ends
ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
```

>[!TAB Roku 2.x]

Chiama `mediaTrackEvent` con `MEDIA_BUFFER_START` quando il lettore entra in uno stato di buffering e `MEDIA_BUFFER_COMPLETE` quando esce:

```brightscript
adb = ADBMobile()

' Buffer starts
adb.mediaTrackEvent(adb.MEDIA_BUFFER_START)

' Buffer ends
adb.mediaTrackEvent(adb.MEDIA_BUFFER_COMPLETE)
```

>[!TAB API Media Collection]

Invia un POST `bufferStart` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "bufferStart"
}
```

>[!ENDTABS]
