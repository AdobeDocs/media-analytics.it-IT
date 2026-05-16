---
title: Posizione del capitolo
description: Imposta l’indice del capitolo all’interno del contenuto. È necessario specificare la posizione del capitolo affinché l'ID del capitolo possa essere generato automaticamente correttamente.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 7%

---


# Posizione del capitolo

>[!BEGINSHADEBOX]

*Questa pagina contiene informazioni sulla raccolta dati per la variabile **Chapter position**. Vedi [Posizione capitolo](/help/reporting/dimensions/chapter-position.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile di posizione del capitolo è l&#39;indice del capitolo all&#39;interno del contenuto, a partire da `1` (tipico) o `0` (a seconda della convenzione). Utilizza un indice stabile per capitolo in modo che lo stesso capitolo venga aggregato tra le sessioni.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.chapter.position` |
| **Campo raccolta XDM** | [`mediaCollection.chapterDetails.index`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.chapter.position` |
| **Obbligatorio** | No (Mobile SDK); Sì (Edge, Media Collection API) |
| **Inviato con** | [Inizio capitolo](/help/implementation/events/chapters/chapter-start.md), chiusura capitolo |

## Web SDK

Imposta `index` all&#39;interno di `mediaCollection.chapterDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview):

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

## Mobile SDK

Passa la posizione del capitolo come secondo argomento a `createChapterObject`.

**iOS (Swift)**

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

**Android (Cotlino)**

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1L,
                                              240.0,
                                              0.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

## Roku (BrightScript)

Imposta `index` in `mediaCollection.chapterDetails` quando chiama `sendMediaEvent` per `media.chapterStart`:

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

## API di Media Edge

Chiama l&#39;endpoint [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) con `index` in `mediaCollection.chapterDetails`:

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

## Media SDK

Passa la posizione del capitolo come secondo argomento a `ADB.Media.createChapterObject`:

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",
  1,
  240,
  0
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

## API Media Collection

Includi `media.chapter.index` nell&#39;oggetto `params` della richiesta POST `chapterStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.index": 1
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento eventi API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md).
