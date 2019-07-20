---
seo-title: Tenere traccia dei capitoli e dei segmenti su iOS
title: Tenere traccia dei capitoli e dei segmenti su iOS
uuid: ffc 5 ce 9 f -04 ba -4059-92 d 4-4 cb 4180 ac 9 ed
translation-type: tm+mt
source-git-commit: b461da1823e45eef86302e14501eac0d4b055c7a

---


# Track chapters and segments on iOS{#track-chapters-and-segments-on-ios}

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

   ```
   id chapterObject =  
     [ADBMediaHeartbeat createChapterObjectWithName:[CHAPTER_NAME] 
                        position:[POSITION] 
                        length:[LENGTH] 
                        startTime:[START_TIME]];
   ```

1. Se includete metadati personalizzati per il capitolo, create le variabili di dati di contesto per i metadati:

   ```
   NSMutableDictionary *chapterDictionary = [[NSMutableDictionary alloc] init]; 
   [chapterDictionary setObject:@"Sample segment type" forKey:@"segmentType"]; 
   [chapterDictionary setObject:@"Sample segment name" forKey:@"segmentName"]; 
   [chapterDictionary setObject:@"Sample segment info" forKey:@"segmentInfo"];
   ```

1. To begin tracking the chapter playback, call the `ChapterStart` event in the `MediaHeartbeat` instance:

   ```
   - (void)onChapterStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterStart  
                        mediaObject:chapterObject     
                        data:chapterDictionary]; 
   }
   ```

1. When playback reaches the chapter end boundary, as defined by your custom code, call the `ChapterComplete` event in the `MediaHeartbeat` instance:

   ```
   - (void)onChapterComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. If chapter playback did not complete because the user chose to skip the chapter (for example, if the user seeks out of the chapter boundary), call the `ChapterSkip` event in the MediaHeartbeat instance:

   ```
   - (void)onChapterSkip:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterSkip  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. In caso di capitoli aggiuntivi, ripetete i passaggi da 1 a 5.

