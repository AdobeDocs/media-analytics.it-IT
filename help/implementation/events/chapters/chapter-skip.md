---
title: Salta capitolo
description: Segnala che il visualizzatore ha saltato un capitolo.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 2%

---


# Salta capitolo

Il capitolo ignora l’evento segnala che il visualizzatore ha saltato un capitolo prima del termine. Inviala quando il visualizzatore passa oltre il limite del capitolo senza guardarlo fino al completamento. Invia [Capitolo completato](chapter-complete.md) se il capitolo viene riprodotto fino alla fine.

* **Prerequisiti**: [Inizio sessione](../session/session-start.md), [Inizio capitolo](chapter-start.md)
* **Metrica associata**: nessuna

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.chapterSkip"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

>[!TAB iOS]

Chiamare `trackEvent` con il tipo di evento `ChapterSkip`.

```swift
tracker.trackEvent(event: MediaEvent.ChapterSkip, info: nil, metadata: nil)
```

>[!TAB Android]

Chiamare `trackEvent` con il tipo di evento `ChapterSkip`.

```kotlin
tracker.trackEvent(Media.Event.ChapterSkip, null, null)
```

>[!TAB Edge Roku]

Chiama `sendMediaEvent` con `eventType: "media.chapterSkip"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterSkip",
        "mediaCollection": {
            "playhead": 60
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [chapterSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterskip):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 60
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

Chiamare `trackEvent` con il tipo di evento `ChapterSkip`:

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterSkip, null, null);
```

>[!TAB Chromecast]

Chiamare `trackEvent` con il tipo di evento `ChapterSkip`:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip);
```

>[!TAB Roku 2.x]

Chiamare `mediaTrackEvent` con il tipo di evento `MEDIA_CHAPTER_SKIP`:

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_CHAPTER_SKIP)
```

>[!TAB API Media Collection]

Invia un POST `chapterSkip` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "chapterSkip"
}
```

>[!ENDTABS]
