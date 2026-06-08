---
title: Nome del capitolo
description: Imposta il nome descrittivo di ciascun capitolo in modo che la generazione rapporti a livello di capitolo possa suddividersi per titolo del capitolo.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 4%

---


# Nome del capitolo

>[!BEGINSHADEBOX]

*In questa pagina è illustrata la raccolta dati per la variabile **Chapter name**. Vedi [Nome capitolo](/help/reporting/dimensions/chapter-name.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile del nome del capitolo è il titolo leggibile di un capitolo, ad esempio `"Pilot Episode - Opening"`. Impostarlo su ogni evento `media.chapterStart` il cui contenuto è diviso in capitoli.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.chapter.friendlyName` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.chapterDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.chapter.friendlyName` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio capitolo](/help/implementation/events/chapters/chapter-start.md), chiusura capitolo |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `friendlyName` all&#39;interno di `xdm.mediaCollection.chapterDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview):

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

Passa il nome del capitolo come primo argomento (`name`) a `createChapterObject`.

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

>[!TAB Android]

Passa il nome del capitolo come primo argomento (`name`) a `createChapterObject`.

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1L,
                                              240.0,
                                              0.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

>[!TAB Edge Roku]

Imposta `friendlyName` in `xdm.mediaCollection.chapterDetails` quando chiama `sendMediaEvent` per `media.chapterStart`:

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

Chiama l&#39;endpoint [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) con `friendlyName` in `xdm.mediaCollection.chapterDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "friendlyName": "Pilot Episode - Opening",
          "index": 1,
          "offset": 0,
          "length": 240
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Passa il nome del capitolo come primo argomento a `ADB.Media.createChapterObject`:

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length (seconds)
  0                           // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

>[!TAB Chromecast]

Passa il nome del capitolo come primo argomento (`name`) a `ADBMobile.media.createChapterObject`:

```javascript
var chapterInfo = ADBMobile.media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length
  0                           // startTime
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, chapterInfo, null);
```

>[!TAB Roku 2.x]

Passa il nome del capitolo come primo argomento (`name`) a `adb_media_init_chapterinfo`:

```brightscript
adb = ADBMobile()
chapterInfo = adb_media_init_chapterinfo("Pilot Episode - Opening", 1, 240.0, 0.0)  ' name, position, length, startTime

adb.mediaTrackEvent(adb.MEDIA_CHAPTER_START, chapterInfo)
```

>[!TAB API Media Collection]

Includi `media.chapter.friendlyName` nell&#39;oggetto `params` della richiesta POST `chapterStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Pilot Episode - Opening"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).

>[!ENDTABS]
