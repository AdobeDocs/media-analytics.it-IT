---
title: Scopri come tenere traccia di capitoli e segmenti su Chromecast
description: Scopri come implementare il tracciamento di capitoli e segmenti utilizzando Media SDK su Chromecast.
uuid: 5ea562b9-0e07-4fbb-9a3b-213d746304f5
exl-id: 26b71e4d-ced7-49cb-a838-2b1c8d4ee4de
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/QT8c6k8HuX2Zd1YLlTd4xlW-M6WUqzwhQtoKLkGiEho
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
source-wordcount: 236
ht-degree: 100%

---

# Tracciare capitoli e segmenti in Chromecast{#track-chapters-and-segments-on-chromecast}

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

   Oggetto capitolo: [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createChapterObject)

   ```js
   chapterInfo = ADBMobile.media.createChapterObject("First Chapter", 1, CHAPTER1_LENGTH, CHAPTER1_START_POS);
   ```

1. Se includi metadati personalizzati per il capitolo, crea le variabili di dati di contesto per i metadati:

   ```js
   var chapterContextData = {
       segmentType: "Sample segment type"
   };
   ```

1. Per iniziare a tenere traccia della riproduzione del capitolo, traccia l’evento `ChapterStart`: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, ChapterInfo, chapterContextData);
   ```

1. Quando la riproduzione raggiunge il limite finale del capitolo, come definito dal codice personalizzato, chiama l’evento `ChapterComplete` nell’istanza `MediaHeartbeat`: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterComplete);
   ```

1. Se la riproduzione del capitolo non è stata completata perché l’utente ha scelto di saltare il capitolo (ad esempio, se l’utente effettua una ricerca fuori dal limite del capitolo), chiama l’evento `ChapterSkip`: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip);
   ```

1. Se ci sono capitoli aggiuntivi, ripeti i punti da 1 a 5.
