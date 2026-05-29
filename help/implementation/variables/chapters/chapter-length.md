---
title: Durata capitolo
description: Imposta la lunghezza di ciascun capitolo, in secondi.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 4%

---


# Durata capitolo

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la raccolta dati per la variabile **Chapter length**. Vedi [Lunghezza capitolo](/help/reporting/dimensions/chapter-length.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile di lunghezza del capitolo è la durata del capitolo, in secondi. Impostarlo su ogni evento `media.chapterStart`.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.chapter.length` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.chapterDetails.length`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.chapter.length` |
| **Obbligatorio** | No (Mobile SDK); Sì (Edge, Media Collection API) |
| **Inviato con** | [Inizio capitolo](/help/implementation/events/chapters/chapter-start.md), chiusura capitolo |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `length` all&#39;interno di `xdm.mediaCollection.chapterDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

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

Passa la lunghezza del capitolo in secondi come terzo argomento a `createChapterObject`.

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

>[!TAB Android]

Passa la lunghezza del capitolo in secondi come terzo argomento a `createChapterObject`.

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1L,
                                              240.0,
                                              0.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

>[!TAB Roku]

Imposta `length` in `xdm.mediaCollection.chapterDetails` quando chiama `sendMediaEvent` per `media.chapterStart`:

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

Chiama l&#39;endpoint [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) con `length` in `xdm.mediaCollection.chapterDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
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

Passa la lunghezza del capitolo come terzo argomento a `ADB.Media.createChapterObject`:

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",
  1,
  240,
  0
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

>[!TAB Chromecast]

Passa la lunghezza del capitolo in secondi come terzo argomento (`length`) a `ADBMobile.media.createChapterObject`:

```javascript
var chapterInfo = ADBMobile.media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length (seconds)
  0                           // startTime
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, chapterInfo, null);
```

>[!TAB API Media Collection]

Includi `media.chapter.length` nell&#39;oggetto `params` della richiesta POST `chapterStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.length": 240
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).

>[!ENDTABS]
