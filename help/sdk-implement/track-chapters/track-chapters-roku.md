---
title: Tracciare capitoli e segmenti su Roku
description: In questo argomento viene descritta l’implementazione del tracciamento di capitoli e segmenti mediante l’SDK per file multimediali su Roku.
uuid: 15c07131-77d7-4a97-92c6-0a190c6b08d3
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Tracciare capitoli e segmenti su Roku{#track-chapters-and-segments-on-roku}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione mediante gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare la Guida per gli sviluppatori qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Implementazione di metadati annuncio standard

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

   ```
   chapterInfo =  
     adb_media_init_chapterinfo(<CHAPTER_NAME>,  
                                <POSITION>,  
                                <LENGTH>,  
                                <START_TIME>);)
   ```

1. Se includete metadati personalizzati per il capitolo, create le variabili di dati di contesto per i metadati:

   ```
   chapterContextData = {} 
   chapterContextData["seg_type"] = "seg_type" 
   chapterContextData["seg_name"] = "seg_name" 
   chapterContextData["seg_info"] = "seg_info"
   ```

1. Per iniziare a monitorare la riproduzione dei capitoli, chiamate l’ `ChapterStart` evento nell’ `MediaHeartbeat` istanza:

   ```
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_START, chapterInfo, chapterContextData)
   ```

1. Quando la riproduzione raggiunge il limite finale del capitolo, come definito dal codice personalizzato, chiamate l’ `ChapterComplete` evento nell’ `MediaHeartbeat` istanza.

   ```
   chapterContextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_COMPLETE, chapterInfo, chapterContextData)
   ```

1. Se la riproduzione del capitolo non è stata completata perché l’utente ha scelto di saltare il capitolo (ad esempio, se l’utente cerca di uscire dal limite del capitolo), chiamate l’ `ChapterSkip` evento nell’istanza MediaHeartbeat.

   ```
   chapterContextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_SKIP, chapterInfo, chapterContextData)
   ```

1. Se sono presenti altri capitoli, ripetete i punti da 1 a 5.

