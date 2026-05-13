---
title: Scopri come Tracciare capitoli e segmenti in Roku
description: Scopri come implementare il tracciamento di capitoli e segmenti utilizzando Media SDK su Roku.
uuid: 15c07131-77d7-4a97-92c6-0a190c6b08d3
exl-id: b5eb8be7-4b85-4ba7-9216-dd691be7ba46
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Z06I7x3nDZvYHoQHo9bcjs4UiS2YR6yN8rwJqG3vX1w
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 203
ht-degree: 98%

---

# Tracciare capitoli e segmenti in Roku{#track-chapters-and-segments-on-roku}

Le istruzioni seguenti forniscono indicazioni per l’implementazione utilizzando gli SDK 2.x.

>[!IMPORTANT]
>
> Se implementi una versione 1.x dell&#39;SDK, puoi scaricare la Guida per gli sviluppatori qui: [Scaricare gli SDK](/help/getting-started/download-sdks.md).

## Implementare metadati standard di annunci

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
   chapterInfo =  
     adb_media_init_chapterinfo(<CHAPTER_NAME>,  
                                <POSITION>,  
                                <LENGTH>,  
                                <START_TIME>);)
   ```

1. Se includi metadati personalizzati per il capitolo, crea le variabili di dati di contesto per i metadati:

   ```
   chapterContextData = {}
   chapterContextData["seg_type"] = "seg_type"
   chapterContextData["seg_name"] = "seg_name"
   chapterContextData["seg_info"] = "seg_info"
   ```

1. Per iniziare a tenere traccia della riproduzione del capitolo, chiama l’evento `ChapterStart` nell’istanza `MediaHeartbeat`.

   ```
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_START, chapterInfo, chapterContextData)
   ```

1. Quando la riproduzione raggiunge il limite finale del capitolo, come definito dal codice personalizzato, chiama l’evento `ChapterComplete` nell’istanza `MediaHeartbeat`.

   ```
   chapterContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_COMPLETE, chapterInfo, chapterContextData)
   ```

1. Se la riproduzione del capitolo non è stata completata perché l’utente ha scelto di saltare il capitolo (ad esempio, se l’utente cerca fuori dal limite del capitolo), chiama l’evento `ChapterSkip` nell’istanza MediaHeartbeat.

   ```
   chapterContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_SKIP, chapterInfo, chapterContextData)
   ```

1. Se ci sono capitoli aggiuntivi, ripeti i punti da 1 a 5.
