---
seo-title: Tracciare capitoli e segmenti su iOS
title: Tracciare capitoli e segmenti su iOS
uuid: ffc5ce9f-04ba-4059-92d4-4cb4180ac9ed
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tracciare capitoli e segmenti su iOS{#track-chapters-and-segments-on-ios}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione mediante gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare la Guida per gli sviluppatori qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

1. Identificare il momento in cui si verifica l’evento di inizio del capitolo e creare l’ `ChapterObject` istanza utilizzando le informazioni sul capitolo.

   `ChapterObject` riferimento tracciamento capitoli:

   >[!NOTE]
   >
   >Queste variabili sono necessarie solo se si prevede di tenere traccia dei capitoli.

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome del capitolo | Sì |
   | `position` | Posizione del capitolo | Sì |
   | `length` | Lunghezza capitolo | Sì |
   | `startTime` | Ora inizio capitolo | Sì |

   Oggetto Chapter:

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

1. Per iniziare a monitorare la riproduzione dei capitoli, chiamate l’ `ChapterStart` evento nell’ `MediaHeartbeat` istanza:

   ```
   - (void)onChapterStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterStart  
                        mediaObject:chapterObject     
                        data:chapterDictionary]; 
   }
   ```

1. Quando la riproduzione raggiunge il limite finale del capitolo, come definito dal codice personalizzato, chiamate l’ `ChapterComplete` evento nell’ `MediaHeartbeat` istanza:

   ```
   - (void)onChapterComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Se la riproduzione del capitolo non è stata completata perché l’utente ha scelto di saltare il capitolo (ad esempio, se l’utente cerca di uscire dal limite del capitolo), chiamate l’ `ChapterSkip` evento nell’istanza MediaHeartbeat:

   ```
   - (void)onChapterSkip:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterSkip  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Se sono presenti altri capitoli, ripetete i punti da 1 a 5.

