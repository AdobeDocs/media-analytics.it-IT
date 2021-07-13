---
title: Come tenere traccia dei capitoli e dei segmenti su Roku
description: Scopri come implementare il tracciamento di capitoli e segmenti utilizzando Media SDK su Roku.
uuid: 15c07131-77d7-4a97-92c6-0a190c6b08d3
exl-id: b5eb8be7-4b85-4ba7-9216-dd691be7ba46
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 4%

---

# Tracciamento capitoli e segmenti su Roku{#track-chapters-and-segments-on-roku}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione tramite SDK 2.x. Se implementi una versione 1.x dell&#39;SDK, puoi scaricare la Guida per gli sviluppatori qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Implementazione dei metadati standard di annunci

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
   chapterInfo =  
     adb_media_init_chapterinfo(<CHAPTER_NAME>,  
                                <POSITION>,  
                                <LENGTH>,  
                                <START_TIME>);)
   ```

1. Se includi metadati personalizzati per il capitolo , crea le variabili di dati di contesto per i metadati:

   ```
   chapterContextData = {} 
   chapterContextData["seg_type"] = "seg_type" 
   chapterContextData["seg_name"] = "seg_name" 
   chapterContextData["seg_info"] = "seg_info"
   ```

1. Per iniziare a tenere traccia della riproduzione del capitolo, chiama l&#39;evento `ChapterStart` nell&#39;istanza `MediaHeartbeat`:

   ```
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_START, chapterInfo, chapterContextData)
   ```

1. Quando la riproduzione raggiunge il limite finale del capitolo, come definito dal codice personalizzato, invoca l&#39;evento `ChapterComplete` nell&#39;istanza `MediaHeartbeat`.

   ```
   chapterContextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_COMPLETE, chapterInfo, chapterContextData)
   ```

1. Se la riproduzione dei capitoli non è stata completata perché l&#39;utente ha scelto di saltare il capitolo (ad esempio, se l&#39;utente cerca fuori dal limite del capitolo), chiamare l&#39;evento `ChapterSkip` nell&#39;istanza MediaHeartbeat.

   ```
   chapterContextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_SKIP, chapterInfo, chapterContextData)
   ```

1. In caso di capitoli aggiuntivi, ripetere i punti da 1 a 5.
