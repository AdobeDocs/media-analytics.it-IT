---
title: Scopri come tracciare capitoli e segmenti su iOS
description: Scopri come implementare il tracciamento di capitoli e segmenti utilizzando Media SDK su iOS.
uuid: ffc5ce9f-04ba-4059-92d4-4cb4180ac9ed
exl-id: ea8a1dd6-043f-41a4-9cef-845da92bfa32
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '195'
ht-degree: 100%

---

# Tracciare capitoli e segmenti su iOS{#track-chapters-and-segments-on-ios}

Le istruzioni seguenti forniscono indicazioni per l’implementazione utilizzando gli SDK 2.x.

>[!IMPORTANT]
>
> Se implementi una versione 1.x dell&#39;SDK, puoi scaricare la Guida per gli sviluppatori qui: [Scaricare gli SDK](/help/getting-started/download-sdks.md).

1. Identifica quando si verifica l’evento di inizio del capitolo e crea l’istanza `ChapterObject` utilizzando le informazioni sul capitolo.

   Riferimento di tracciamento dei capitoli `ChapterObject`:

   >[!NOTE]
   >
   >Queste variabili sono necessarie solo se intendi tenere traccia dei capitoli.

   | Nome variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome del capitolo | Sì |
   | `position` | Posizione del capitolo | Sì |
   | `length` | Durata capitolo | Sì |
   | `startTime` | Ora di inizio capitolo | Sì |

   Oggetto capitolo:

   ```
   id chapterObject =  
     [ADBMediaHeartbeat createChapterObjectWithName:[CHAPTER_NAME]
                        position:[POSITION]
                        length:[LENGTH]
                        startTime:[START_TIME]];
   ```

1. Se includi metadati personalizzati per il capitolo, crea le variabili di dati di contesto per i metadati:

   ```
   NSMutableDictionary *chapterDictionary = [[NSMutableDictionary alloc] init];
   [chapterDictionary setObject:@"Sample segment type" forKey:@"segmentType"];
   [chapterDictionary setObject:@"Sample segment name" forKey:@"segmentName"];
   [chapterDictionary setObject:@"Sample segment info" forKey:@"segmentInfo"];
   ```

1. Per iniziare a tenere traccia della riproduzione del capitolo, chiama l’evento `ChapterStart` nell’istanza `MediaHeartbeat`.

   ```
   - (void)onChapterStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterStart  
                        mediaObject:chapterObject     
                        data:chapterDictionary];
   }
   ```

1. Quando la riproduzione raggiunge il limite finale del capitolo, come definito dal codice personalizzato, chiama l’evento `ChapterComplete` nell’istanza `MediaHeartbeat`.

   ```
   - (void)onChapterComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. Se la riproduzione del capitolo non è stata completata perché l’utente ha scelto di saltare il capitolo (ad esempio, se l’utente effettua una ricerca fuori dal limite del capitolo), chiama l’evento `ChapterSkip` nell’istanza MediaHeartbeat:

   ```
   - (void)onChapterSkip:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterSkip  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. Se ci sono capitoli aggiuntivi, ripeti i punti da 1 a 5.
