---
seo-title: Tenere traccia dei capitoli e dei segmenti in javascript
title: Tenere traccia dei capitoli e dei segmenti in javascript
uuid: ef 99 edf 7-7 a 77-46 c 4-8429-bc 9 a 856 b 98 d 6
translation-type: tm+mt
source-git-commit: b461da1823e45eef86302e14501eac0d4b055c7a

---


# Track chapters and segments on JavaScript{#track-chapters-and-segments-on-javascript}

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

   Oggetto capitolo:

   ```js
   var chapterInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. Se includete metadati personalizzati per il capitolo, create le variabili di dati di contesto per i metadati:

   ```js
   var chapterCustomMetadata = { 
       segmentType: "Sample segment type",  
       segmentName: "Sample segment name",  
       segmentInfo: "Sample segment info" 
   };
   ```

1. To begin tracking the chapter playback, call the `ChapterStart` event in the `MediaHeartbeat` instance:

   ```js
   _onChapterStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                       chapterObject,  
                                       chapterCustomMetadata); 
   };
   ```

1. When playback reaches the chapter end boundary, as defined by your custom code, call the `ChapterComplete` event in the `MediaHeartbeat` instance:

   ```js
   _onChapterComplete = function() { 
      this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
   };
   ```

1. If chapter playback did not complete because the user chose to skip the chapter (for example, if the user seeks out of the chapter boundary), call the `ChapterSkip` event in the MediaHeartbeat instance:

   ```js
   _onChapterSkip = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
   };
   ```

1. In caso di capitoli aggiuntivi, ripetete i passaggi da 1 a 5.

