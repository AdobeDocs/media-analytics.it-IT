---
title: Scopri come tenere traccia di capitoli e segmenti su iOS
description: Scopri come implementare il tracciamento di capitoli e segmenti utilizzando Media SDK su iOS.
uuid: ffc5ce9f-04ba-4059-92d4-4cb4180ac9ed
exl-id: ea8a1dd6-043f-41a4-9cef-845da92bfa32
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 5%

---

# Tracciamento capitoli e segmenti su iOS{#track-chapters-and-segments-on-ios}

Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione tramite SDK 2.x.

>[!IMPORTANT]
>
> Se implementi una versione 1.x dell&#39;SDK, puoi scaricare la Guida per gli sviluppatori qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

1. Identificare quando si verifica l&#39;evento di inizio del capitolo e creare l&#39;istanza `ChapterObject` utilizzando le informazioni del capitolo.

   `ChapterObject` riferimento di tracciamento dei capitoli:

   >[!NOTE]
   >
   >Queste variabili sono necessarie solo se intendi tenere traccia dei capitoli.

   | Nome variable | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome del capitolo | Sì |
   | `position` | Posizione del capitolo | Sì |
   | `length` | Lunghezza del capitolo | Sì |
   | `startTime` | Ora di inizio capitolo | Sì |

   Oggetto capitolo:

   ```
   id chapterObject =  
     [ADBMediaHeartbeat createChapterObjectWithName:[CHAPTER_NAME]
                        position:[POSITION]
                        length:[LENGTH]
                        startTime:[START_TIME]];
   ```

1. Se includi metadati personalizzati per il capitolo , crea le variabili di dati di contesto per i metadati:

   ```
   NSMutableDictionary *chapterDictionary = [[NSMutableDictionary alloc] init];
   [chapterDictionary setObject:@"Sample segment type" forKey:@"segmentType"];
   [chapterDictionary setObject:@"Sample segment name" forKey:@"segmentName"];
   [chapterDictionary setObject:@"Sample segment info" forKey:@"segmentInfo"];
   ```

1. Per iniziare a tenere traccia della riproduzione del capitolo, chiama l&#39;evento `ChapterStart` nell&#39;istanza `MediaHeartbeat`:

   ```
   - (void)onChapterStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterStart  
                        mediaObject:chapterObject     
                        data:chapterDictionary];
   }
   ```

1. Quando la riproduzione raggiunge il limite finale del capitolo, come definito dal codice personalizzato, invoca l&#39;evento `ChapterComplete` nell&#39;istanza `MediaHeartbeat`:

   ```
   - (void)onChapterComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. Se la riproduzione del capitolo non è stata completata perché l&#39;utente ha scelto di saltare il capitolo (ad esempio, se l&#39;utente cerca fuori dal limite del capitolo), chiamare l&#39;evento `ChapterSkip` nell&#39;istanza MediaHeartbeat:

   ```
   - (void)onChapterSkip:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterSkip  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. In caso di capitoli aggiuntivi, ripetere i punti da 1 a 5.
