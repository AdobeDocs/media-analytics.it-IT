---
seo-title: Panoramica
title: Panoramica
uuid: 3 fe 32425-5 e 2 a -4886-8 fea-d 91 d 15671 bb 0
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Panoramica{#overview}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione con SDK 2. x. Se implementhi una versione 1. x dell'SDK, puoi scaricare la Guida sviluppatori qui: [Scarica gli SDK.](/help/sdk-implement/download-sdks.md)

I capitoli e il tracciamento dei segmenti sono disponibili per capitoli o segmenti di supporti personalizzati. Alcuni usi comuni per il tracciamento dei capitoli sono per definire segmenti personalizzati basati sul contenuto multimediale (come ad esempio il baseball innings) o per definire segmenti di contenuto tra interruzioni pubblicitarie. Il tracciamento dei capitoli **non** è richiesto per le implementazioni di tracciamento dei contenuti multimediali principali.

Il tracciamento dei capitoli include l'avvio del capitolo, il completamento del capitolo e l'eliminazione del capitolo. Puoi utilizzare l'API del lettore multimediale con logica di segmentazione personalizzata per identificare gli eventi dei capitoli e compilare le variabili di capitolo richieste e facoltative.

## Eventi del lettore

### Inizio capitolo

* Create l'istanza di oggetto capitoli per il capitolo, `chapterObject`
* Compilare i metadati del capitolo, `chapterCustomMetadata`
* Chiamata `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### Completato il capitolo

* Chiamata `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### Salta nel capitolo

* Chiamata `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implementare il tracciamento dei capitoli {#section_52221B3A9BFD46B3A22DA6BCE97CCD75}

1. Identificare l'evento di inizio del capitolo e creare l' `ChapterObject` istanza utilizzando le informazioni sul capitolo.

   Di seguito è riportato `ChapterObject` il riferimento di tracciamento dei capitoli:

   >[!NOTE]
   >
   >Queste variabili sono necessarie solo se prevedete di tenere traccia dei capitoli.

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome capitolo | Sì |
   | `position` | Posizione capitolo | Sì |
   | `length` | Lunghezza capitolo | Sì |
   | `startTime` | Ora di inizio capitolo | Sì |

1. Se includete metadati personalizzati per il capitolo, create le variabili di dati di contesto per i metadati.
1. Per iniziare a tracciare la riproduzione del capitolo, richiamare l' `ChapterStart` evento nell `MediaHeartbeat` 'istanza.
1. Quando la riproduzione raggiunge il bordo finale del capitolo, come definito dal codice personalizzato, chiamate l' `ChapterComplete` evento nell `MediaHeartbeat` 'istanza.
1. Se la riproduzione dei capitoli non è stata completata perché l'utente ha scelto di ignorare il capitolo (ad esempio, se l'utente cerca il limite dei capitoli), chiama l' `ChapterSkip` evento nell'istanza mediaheartbeat.
1. In caso di capitoli aggiuntivi, ripetete i passaggi da 1 a 5.

Il seguente codice di esempio utilizza l'SDK javascript 2. x per un lettore multimediale HTML 5. Utilizzate questo codice con il codice di riproduzione multimediale principale.

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

