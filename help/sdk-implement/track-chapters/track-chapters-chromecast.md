---
seo-title: Tracciare capitoli e segmenti su Chromecast
title: Tracciare capitoli e segmenti su Chromecast
uuid: 5 ea 562 b 9-0 e 07-4 fbb -9 a 3 b -213 d 746304 f 5
translation-type: tm+mt
source-git-commit: b461da1823e45eef86302e14501eac0d4b055c7a

---


# Track chapters and segments on Chromecast{#track-chapters-and-segments-on-chromecast}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione con SDK 2. x. If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [Download SDKs.](../../sdk-implement/download-sdks.md)

1. Identify when the chapter start event occurs and create the `ChapterObject` instance by using the chapter information.

   `ChapterObject` riferimento di tracciamento dei capitoli:

   >[!NOTE]
   >
   >Queste variabili sono necessarie solo se prevedete di tenere traccia dei capitoli.

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome capitolo | Sì |
   | `position` | Posizione capitolo | Sì |
   | `length` | Lunghezza capitolo | Sì |
   | `startTime` | Ora di inizio capitolo | Sì |

   Chapter object: [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createChapterObject)

   ```js
   chapterInfo = ADBMobile.media.createChapterObject("First Chapter", 1, CHAPTER1_LENGTH, CHAPTER1_START_POS);
   ```

1. Se includete metadati personalizzati per il capitolo, create le variabili di dati di contesto per i metadati:

   ```js
   var chapterContextData = { 
       segmentType: "Sample segment type" 
   };
   ```

1. To begin tracking the chapter playback, track the `ChapterStart` event: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, ChapterInfo, chapterContextData); 
   ```

1. When playback reaches the chapter end boundary, as defined by your custom code, call the `ChapterComplete` event in the `MediaHeartbeat` instance: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterComplete);
   ```

1. If chapter playback did not complete because the user chose to skip the chapter (for example, if the user seeks out of the chapter boundary), track the `ChapterSkip` event: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip); 
   ```

1. In caso di capitoli aggiuntivi, ripetete i passaggi da 1 a 5.

