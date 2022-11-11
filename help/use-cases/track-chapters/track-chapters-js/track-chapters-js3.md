---
title: Scopri come tenere traccia di capitoli e segmenti utilizzando JavaScript 3.x
description: Scopri come implementare il tracciamento di capitoli e segmenti utilizzando Media SDK nelle app del browser (JS).
exl-id: 00ba11df-d226-45a2-a561-dc9f15dcf714
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 47%

---

# Tracciamento capitoli e segmenti con JavaScript 3.x{#track-chapters-and-segments-on-javascript}

Le istruzioni seguenti forniscono indicazioni per l’implementazione tramite SDK 3.x.

>[!IMPORTANT]
>
> Se implementi una versione precedente dell’SDK, puoi scaricare la Guida per gli sviluppatori qui: [Scaricare gli SDK.](/help/getting-started/download-sdks.md)

1. Identifica quando si verifica l’evento di inizio del capitolo e crea l’istanza `ChapterObject` utilizzando le informazioni del capitolo.

   `ChapterObject` riferimento di tracciamento dei capitoli:

   >[!NOTE]
   >
   >Queste variabili sono necessarie solo se intendi tenere traccia dei capitoli.

   | Nome variabile | Tipo | Descrizione |
   | --- | --- | --- |
   | `name` | stringa | Stringa non vuota che indica il nome del capitolo. |
   | `position` | numero | La posizione del capitolo all’interno del contenuto, a partire da 1. |
   | `length` | numero | Numero positivo che indica la lunghezza del capitolo. |
   | `startTime` | numero | Valore della testina all&#39;inizio del capitolo. |

   Oggetto capitolo:

   ```js
   var chapterObject =
     ADB.Media.createChapterObject.createChapterObject(<CHAPTER_NAME>,
                                        <POSITION>,
                                        <LENGTH>,
                                        <START_TIME>);
   ```

1. Se includi metadati personalizzati per il capitolo, crea le variabili di dati di contesto per i metadati:

   ```js
   var chapterMetadata = {};
   chapterMetadata["segmentType"] = "Sample segment type";
   ```

1. Per iniziare a tenere traccia della riproduzione del capitolo, chiamare il `ChapterStart` evento `MediaHeartbeat` istanza:

   ```js
   _onChapterStart = function() {
     tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);
   
   };
   ```

1. Quando la riproduzione raggiunge il limite finale del capitolo, come definito dal codice personalizzato, chiama il `ChapterComplete` evento `MediaHeartbeat` istanza:

   ```js
   _onChapterComplete = function() {
      tracker.trackEvent(ADB.Media.Event.ChapterComplete);
   };
   ```

1. Se la riproduzione del capitolo non è stata completata perché l’utente ha scelto di saltare il capitolo (ad esempio, se l’utente cerca fuori dal limite del capitolo), chiama l’evento `ChapterSkip` nell’istanza MediaHeartbeat:

   ```js
   _onChapterSkip = function() {
       tracker.trackEvent(ADB.Media.Event.ChapterSkip);
   };
   ```

1. In caso di capitoli aggiuntivi, ripetere i punti da 1 a 5.
