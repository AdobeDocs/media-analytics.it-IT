---
title: Tracciare capitoli e segmenti utilizzando JavaScript 3.x
description: Questo argomento descrive l’implementazione del tracciamento di capitoli e segmenti mediante l’SDK per file multimediali nelle app browser (JS).
translation-type: tm+mt
source-git-commit: b14b56aea4a1821a2a160b9cd301cd181f1ba8dd
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 1%

---


# Tracciare capitoli e segmenti utilizzando JavaScript 3.x{#track-chapters-and-segments-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione mediante gli SDK 3.x. Se stai implementando versioni precedenti dell’SDK, puoi scaricare la Guida per gli sviluppatori qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

1. Identificare il momento in cui si verifica l’evento di inizio del capitolo e creare l’ `ChapterObject` istanza utilizzando le informazioni sul capitolo.

   `ChapterObject` riferimento tracciamento capitoli:

   >[!NOTE]
   >
   >Queste variabili sono necessarie solo se si prevede di tenere traccia dei capitoli.

   | Nome della variabile | Tipo | Descrizione |
   | --- | --- | --- |
   | `name` | string | Stringa non vuota che denota il nome del capitolo. |
   | `position` | number | La posizione del capitolo all&#39;interno del contenuto, a partire da 1. |
   | `length` | number | Numero positivo che indica la lunghezza del capitolo. |
   | `startTime` | number | Valore della testina di riproduzione all&#39;inizio del capitolo. |

   Oggetto Chapter:

   ```js
   var chapterObject =
     ADB.Media.createChapterObject.createChapterObject(<CHAPTER_NAME>,
                                        <POSITION>,
                                        <LENGTH>,
                                        <START_TIME>);
   ```

1. Se includete metadati personalizzati per il capitolo, create le variabili di dati di contesto per i metadati:

   ```js
   var chapterMetadata = {};
   chapterMetadata["segmentType"] = "Sample segment type";
   ```

1. Per iniziare a monitorare la riproduzione dei capitoli, chiamate l’ `ChapterStart` evento nell’ `MediaHeartbeat` istanza:

   ```js
   _onChapterStart = function() {
     tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);
   
   };
   ```

1. Quando la riproduzione raggiunge il limite finale del capitolo, come definito dal codice personalizzato, chiamate l’ `ChapterComplete` evento nell’ `MediaHeartbeat` istanza:

   ```js
   _onChapterComplete = function() {
      tracker.trackEvent(ADB.Media.Event.ChapterComplete);
   };
   ```

1. Se la riproduzione del capitolo non è stata completata perché l’utente ha scelto di saltare il capitolo (ad esempio, se l’utente cerca di uscire dal limite del capitolo), chiamate l’ `ChapterSkip` evento nell’istanza MediaHeartbeat:

   ```js
   _onChapterSkip = function() {
       tracker.trackEvent(ADB.Media.Event.ChapterSkip);
   };
   ```

1. Se sono presenti altri capitoli, ripetete i punti da 1 a 5.
