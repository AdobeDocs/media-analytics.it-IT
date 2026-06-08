---
title: Inizio capitolo
description: Segnala l’inizio di un segmento di capitolo all’interno del contenuto.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 2%

---


# Inizio capitolo

L’evento di inizio capitolo segnala l’inizio di un capitolo all’interno del contenuto. Il tracciamento dei capitoli è facoltativo e non obbligatorio per il tracciamento dei contenuti multimediali di base. I capitoli non possono sovrapporsi; invia [Capitolo completato](chapter-complete.md) o [Capitolo ignorato](chapter-skip.md) per chiudere il capitolo corrente prima di avviarne uno nuovo.

* **Prerequisiti**: [Inizio sessione](../session/session-start.md)
* **Metrica associata**: [[!UICONTROL Chapter starts]](/help/reporting/metrics/chapter-starts.md)

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.chapterStart"` e il `chapterDetails` richiesto:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Pilot Episode - Opening",
        index: 1,
        offset: 0,
        length: 240
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passa il nome del capitolo, la posizione, la lunghezza e l&#39;ora di inizio a `createChapterObject`, quindi chiama `trackEvent`.

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

>[!TAB Android]

Passa il nome del capitolo, la posizione, la lunghezza e l&#39;ora di inizio a `createChapterObject`, quindi chiama `trackEvent`.

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1,
                                              240,
                                              0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

>[!TAB Edge Roku]

Chiama `sendMediaEvent` con `eventType: "media.chapterStart"` e il `chapterDetails` richiesto:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Pilot Episode - Opening",
                "index": 1,
                "offset": 0,
                "length": 240
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) con `chapterDetails` richiesto:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "chapterDetails": {
          "index": 1,
          "length": 240,
          "offset": 0
        }
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

Passa il nome del capitolo, la posizione, la lunghezza e l&#39;ora di inizio a `ADB.Media.createChapterObject`:

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length (seconds)
  0                           // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, null);
```

>[!TAB Chromecast]

Passa il nome del capitolo, la posizione, la lunghezza e l&#39;ora di inizio a `ADBMobile.media.createChapterObject`:

```javascript
var chapterInfo = ADBMobile.media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length (seconds)
  0                           // start time (seconds)
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, chapterInfo, null);
```

>[!TAB Roku 2.x]

Genera un oggetto capitolo con `adb_media_init_chapterinfo`, quindi tieni traccia dell&#39;evento:

```brightscript
adb = ADBMobile()
chapterInfo = adb_media_init_chapterinfo("Pilot Episode - Opening", 1, 240.0, 0.0)  ' name, position, length, startTime

adb.mediaTrackEvent(adb.MEDIA_CHAPTER_START, chapterInfo)
```

>[!TAB API Media Collection]

Invia un POST `chapterStart` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Pilot Episode - Opening",
    "media.chapter.index": 1,
    "media.chapter.offset": 0,
    "media.chapter.length": 240
  }
}
```

>[!ENDTABS]
