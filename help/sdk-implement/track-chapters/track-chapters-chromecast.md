---
title: Tracciare capitoli e segmenti su Chromecast
description: In questo argomento viene descritta l’implementazione del tracciamento di capitoli e segmenti mediante l’SDK per file multimediali su Chromecast.
uuid: 5ea562b9-0e07-4fbb-9a3b-213d746304f5
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Tracciare capitoli e segmenti su Chromecast{#track-chapters-and-segments-on-chromecast}

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

   Oggetto Chapter: [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createChapterObject)

   ```js
   chapterInfo = ADBMobile.media.createChapterObject("First Chapter", 1, CHAPTER1_LENGTH, CHAPTER1_START_POS);
   ```

1. Se includete metadati personalizzati per il capitolo, create le variabili di dati di contesto per i metadati:

   ```js
   var chapterContextData = { 
       segmentType: "Sample segment type" 
   };
   ```

1. Per iniziare a monitorare la riproduzione dei capitoli, tracciate l’ `ChapterStart` evento: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, ChapterInfo, chapterContextData); 
   ```

1. Quando la riproduzione raggiunge il limite finale del capitolo, come definito dal codice personalizzato, chiamate l’ `ChapterComplete` evento nell’ `MediaHeartbeat` istanza: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterComplete);
   ```

1. Se la riproduzione dei capitoli non è stata completata perché l’utente ha scelto di saltare il capitolo (ad esempio, se l’utente cerca di uscire dal limite del capitolo), tracciate l’ `ChapterSkip` evento: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip); 
   ```

1. Se sono presenti altri capitoli, ripetete i punti da 1 a 5.

