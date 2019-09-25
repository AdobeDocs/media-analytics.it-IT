---
seo-title: Tracciare capitoli e segmenti in JavaScript
title: Tracciare capitoli e segmenti in JavaScript
uuid: ef99edf7-7a77-46c4-8429-bc9a856b98d6
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tracciare capitoli e segmenti in JavaScript{#track-chapters-and-segments-on-javascript}

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

   ```js
   var chapterInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. Se includete metadati personalizzati per il capitolo, create le variabili di dati di contesto per i metadati:

   ```js
   var chapterCustomMetadata = { 
       segmentType: "Sample segment type",  
       segmentName: "Sample segment name",  
       segmentInfo: "Sample segment info" 
   };
   ```

1. Per iniziare a monitorare la riproduzione dei capitoli, chiamate l’ `ChapterStart` evento nell’ `MediaHeartbeat` istanza:

   ```js
   _onChapterStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                       chapterObject,  
                                       chapterCustomMetadata); 
   };
   ```

1. Quando la riproduzione raggiunge il limite finale del capitolo, come definito dal codice personalizzato, chiamate l’ `ChapterComplete` evento nell’ `MediaHeartbeat` istanza:

   ```js
   _onChapterComplete = function() { 
      this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
   };
   ```

1. Se la riproduzione del capitolo non è stata completata perché l’utente ha scelto di saltare il capitolo (ad esempio, se l’utente cerca di uscire dal limite del capitolo), chiamate l’ `ChapterSkip` evento nell’istanza MediaHeartbeat:

   ```js
   _onChapterSkip = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
   };
   ```

1. Se sono presenti altri capitoli, ripetete i punti da 1 a 5.

