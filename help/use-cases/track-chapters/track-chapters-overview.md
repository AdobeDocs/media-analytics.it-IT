---
title: Scopri come tenere traccia di capitoli e segmenti
description: Come implementare il tracciamento di capitoli e segmenti con l’SDK per contenuti multimediali.
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 100%

---

# Panoramica {#overview}

Le istruzioni seguenti forniscono indicazioni per l’implementazione tramite SDK 2.x.

>[!IMPORTANT]
> 
> Se implementi una versione 1.x dell&#39;SDK, puoi scaricare la Guida per gli sviluppatori qui: [Scaricare gli SDK](/help/getting-started/download-sdks.md).

Il tracciamento di capitoli e segmenti è disponibile per capitoli o segmenti multimediali personalizzati. Alcuni utilizzi comuni per il tracciamento dei capitoli sono la definizione di segmenti personalizzati in base ai contenuti multimediali (ad esempio gli inning di baseball) o la definizione di segmenti di contenuto tra interruzioni di annunci. Il tracciamento dei capitoli **not** è richiesto per le implementazioni di tracciamento dei contenuti multimediali di base.

Il tracciamento dei capitoli include gli inizi dei capitoli, i completamenti dei capitoli e i salti dei capitoli. Puoi utilizzare l’API del lettore multimediale con logica di segmentazione personalizzata per identificare gli eventi dei capitoli e popolare le variabili dei capitoli richieste e facoltative.

## Eventi del lettore

### All’inizio del capitolo

* Creare l’istanza dell’oggetto capitolo per il capitolo, `chapterObject`
* Compilare i metadati del capitolo, `chapterCustomMetadata`
* Chiamata `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### Al capitolo completo

* Chiamata `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### Salto capitolo

* Chiamata `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implementare il tracciamento dei capitoli {#implement-chapter-tracking}

1. Identifica quando si verifica l’evento di inizio del capitolo e crea l’istanza `ChapterObject` utilizzando le informazioni del capitolo.

   Qui è il riferimento di tracciamento del capitolo `ChapterObject`:

   >[!NOTE]
   >
   >Queste variabili sono necessarie solo se intendi tenere traccia dei capitoli.

   | Nome variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome del capitolo | Sì |
   | `position` | Posizione del capitolo | Sì |
   | `length` | Durata capitolo | Sì |
   | `startTime` | Ora di inizio capitolo | Sì |

1. Se includi metadati personalizzati per il capitolo, crea le variabili di dati di contesto per i metadati.
1. Per iniziare a tenere traccia della riproduzione del capitolo, chiamare l’evento `ChapterStart` nell’istanza `MediaHeartbeat`.
1. Quando la riproduzione raggiunge il limite finale del capitolo, come definito dal codice personalizzato, chiama l’evento `ChapterComplete` nell’istanza `MediaHeartbeat`.
1. Se la riproduzione del capitolo non è stata completata perché l’utente ha scelto di saltare il capitolo (ad esempio, se l’utente cerca fuori dal limite del capitolo), chiama l’evento `ChapterSkip` nell’istanza MediaHeartbeat.
1. In caso di capitoli aggiuntivi, ripetere i punti da 1 a 5.

Il codice di esempio seguente utilizza l’SDK JavaScript 2.x per un lettore multimediale HTML5. Usa questo codice con il codice di riproduzione del contenuto multimediale principale.

```js
/* Call on chapter start */
if (e.type == "chapter start") {
    var chapterObject = MediaHeartbeat.createChapterObject("Inning 5",5,500,2500);
    /* Set custom context data*/
    var chapterCustomMetadata = {
        segmentType:"Baseball Innings",
        segmentName:"Inning 5",
        segmentInfo:"Game Six"
    }
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                   chapterObject,  
                                   chapterCustomMetadata);
};

/* Call on chapter complete */
if (e.type == "chapter complete") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete);
};

/* Call on chapter skip */
if (e.type == "chapter skip") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip);
};
```
