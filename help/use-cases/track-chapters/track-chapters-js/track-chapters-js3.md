---
title: Scopri come tracciare capitoli e segmenti utilizzando JavaScript 3.x
description: Scopri come implementare il tracciamento di capitoli e segmenti utilizzando Media SDK nelle app del browser (JS).
exl-id: 00ba11df-d226-45a2-a561-dc9f15dcf714
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '218'
ht-degree: 100%

---

# Tracciare capitoli e segmenti utilizzando JavaScript 3.x{#track-chapters-and-segments-on-javascript}

Le istruzioni seguenti forniscono indicazioni per l’implementazione utilizzando gli SDK 3.x.

>[!IMPORTANT]
>
> Se implementi una versione precedente dell’SDK, puoi scaricare le Guide per sviluppatori qui: [Scaricare gli SDK.](/help/getting-started/download-sdks.md)

1. Identifica quando si verifica l’evento di inizio del capitolo e crea l’istanza `ChapterObject` utilizzando le informazioni sul capitolo.

   Riferimento di tracciamento dei capitoli `ChapterObject`:

   >[!NOTE]
   >
   >Queste variabili sono necessarie solo se intendi tenere traccia dei capitoli.

   | Nome variabile | Tipo | Descrizione |
   | --- | --- | --- |
   | `name` | string | Stringa non vuota che denota il nome del capitolo. |
   | `position` | number | La posizione numerica del capitolo all’interno del contenuto, a partire da 1. |
   | `length` | number | Numero positivo che indica la lunghezza del capitolo. |
   | `startTime` | number | Valore della testina di riproduzione all’inizio del capitolo. |

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

1. Per iniziare a tenere traccia della riproduzione del capitolo, chiama l’evento `ChapterStart` nell’istanza `MediaHeartbeat`.

   ```js
   _onChapterStart = function() {
     tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);
   
   };
   ```

1. Quando la riproduzione raggiunge il limite finale del capitolo, come definito dal codice personalizzato, chiama l’evento `ChapterComplete` nell’istanza `MediaHeartbeat`.

   ```js
   _onChapterComplete = function() {
      tracker.trackEvent(ADB.Media.Event.ChapterComplete);
   };
   ```

1. Se la riproduzione del capitolo non è stata completata perché l’utente ha scelto di saltare il capitolo (ad esempio, se l’utente effettua una ricerca fuori dal limite del capitolo), chiama l’evento `ChapterSkip` nell’istanza MediaHeartbeat:

   ```js
   _onChapterSkip = function() {
       tracker.trackEvent(ADB.Media.Event.ChapterSkip);
   };
   ```

1. Se ci sono capitoli aggiuntivi, ripeti i punti da 1 a 5.
