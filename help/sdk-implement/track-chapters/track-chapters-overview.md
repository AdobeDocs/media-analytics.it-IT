---
seo-title: Panoramica
title: Panoramica
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Panoramica{#overview}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione mediante gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare la Guida per gli sviluppatori qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

Il tracciamento dei capitoli e dei segmenti è disponibile per capitoli o segmenti multimediali definiti personalizzati. Alcuni usi comuni per il tracciamento dei capitoli sono la definizione di segmenti personalizzati in base al contenuto multimediale (ad esempio, inserzioni di baseball) o la definizione di segmenti di contenuto tra interruzioni di annunci. Il tracciamento dei capitoli **non** è richiesto per le implementazioni di tracciamento dei supporti di base.

Il tracciamento dei capitoli include gli inizi dei capitoli, i completamenti dei capitoli e gli spostamenti dei capitoli. Potete utilizzare l'API Media Player con logica di segmentazione personalizzata per identificare gli eventi dei capitoli e per compilare le variabili dei capitoli richieste e facoltative.

## Eventi del lettore

### Inizio capitolo

* Creare l’istanza dell’oggetto capitolo per il capitolo, `chapterObject`
* Compilate i metadati del capitolo, `chapterCustomMetadata`
* Chiamata `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### Il capitolo completo

* Chiamata `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### Al salto del capitolo

* Chiamata `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implementare il tracciamento dei capitoli {#section_52221B3A9BFD46B3A22DA6BCE97CCD75}

1. Identificare il momento in cui si verifica l’evento di inizio del capitolo e creare l’ `ChapterObject` istanza utilizzando le informazioni sul capitolo.

   Di seguito è riportato il riferimento per il tracciamento dei `ChapterObject` capitoli:

   >[!NOTE]
   >
   >Queste variabili sono necessarie solo se si prevede di tenere traccia dei capitoli.

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome del capitolo | Sì |
   | `position` | Posizione del capitolo | Sì |
   | `length` | Lunghezza capitolo | Sì |
   | `startTime` | Ora inizio capitolo | Sì |

1. Se includete metadati personalizzati per il capitolo, create le variabili di dati di contesto per i metadati.
1. Per iniziare a monitorare la riproduzione del capitolo, chiamate l’ `ChapterStart` evento nell’ `MediaHeartbeat` istanza.
1. Quando la riproduzione raggiunge il limite finale del capitolo, come definito dal codice personalizzato, chiamate l’ `ChapterComplete` evento nell’ `MediaHeartbeat` istanza.
1. Se la riproduzione del capitolo non è stata completata perché l’utente ha scelto di saltare il capitolo (ad esempio, se l’utente cerca di uscire dal limite del capitolo), chiamate l’ `ChapterSkip` evento nell’istanza MediaHeartbeat.
1. Se sono presenti altri capitoli, ripetete i punti da 1 a 5.

Il codice di esempio seguente utilizza l’SDK JavaScript 2.x per un lettore multimediale HTML5. Utilizzare questo codice con il codice di riproduzione del contenuto multimediale di base.

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

