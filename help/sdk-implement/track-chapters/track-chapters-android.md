---
title: Scopri come tenere traccia di capitoli e segmenti su Android
description: Scopri come implementare il tracciamento di capitoli e segmenti utilizzando Media SDK su Android.
uuid: 013815d7-4d9e-48f4-a2b9-3b70cb1149d3
exl-id: ada2e2a7-1383-471c-9ce6-c82ea93fa79d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 5%

---

# Tracciamento capitoli e segmenti su Android{#track-chapters-and-segments-on-android}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione tramite SDK 2.x. Se implementi una versione 1.x dell&#39;SDK, puoi scaricare la Guida per gli sviluppatori qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Implementare il tracciamento dei capitoli

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

   ```java
   MediaObject chapterDataInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. Se includi metadati personalizzati per il capitolo , crea le variabili di dati di contesto per i metadati:

   ```java
   HashMap<String, String> chapterMetadata =  
     new HashMap<String,String>(); 
   chapterMetadata.put("segmentType", "Sample Segment Type"); 
   chapterMetadata.put("segmentName", "Sample Segment Name"); 
   chapterMetadata.put("segmentInfo", "Sample Segment Info");
   ```

1. Per iniziare a tenere traccia della riproduzione del capitolo, chiama l&#39;evento `ChapterStart` nell&#39;istanza `MediaHeartbeat`:

   ```java
   public void onChapterStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                             chapterDataInfo,  
                             chapterMetadata); 
   }
   ```

1. Quando la riproduzione raggiunge il limite finale del capitolo, come definito dal codice personalizzato, invoca l&#39;evento `ChapterComplete` nell&#39;istanza `MediaHeartbeat`:

   ```java
   public void onChapterComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete, null, null); 
   }
   ```

1. Se la riproduzione del capitolo non è stata completata perché l&#39;utente ha scelto di saltare il capitolo (ad esempio, se l&#39;utente cerca fuori dal limite del capitolo), chiamare l&#39;evento `ChapterSkip` nell&#39;istanza MediaHeartbeat:

   ```java
   public void onChapterSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip, null, null); 
   }
   ```

1. In caso di capitoli aggiuntivi, ripetere i punti da 1 a 5.
