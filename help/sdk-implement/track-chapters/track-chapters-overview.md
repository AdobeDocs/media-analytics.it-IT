---
seo-title: Panoramica
title: Panoramica
uuid: 3 fe 32425-5 e 2 a -4886-8 fea-d 91 d 15671 bb 0
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Panoramica{#overview}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione con SDK 2. x. If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

I capitoli e il tracciamento dei segmenti sono disponibili per capitoli o segmenti di supporti personalizzati. Alcuni usi comuni per il tracciamento dei capitoli sono per definire segmenti personalizzati basati sul contenuto multimediale (come ad esempio il baseball innings) o per definire segmenti di contenuto tra interruzioni pubblicitarie. Chapter tracking is **not** required for core media tracking implementations.

Il tracciamento dei capitoli include l'avvio del capitolo, il completamento del capitolo e l'eliminazione del capitolo. Puoi utilizzare l'API del lettore multimediale con logica di segmentazione personalizzata per identificare gli eventi dei capitoli e compilare le variabili di capitolo richieste e facoltative.

## Eventi del lettore

### Inizio capitolo

* Create the chapter object instance for the chapter, `chapterObject`
* Populate the chapter metadata, `chapterCustomMetadata`
* Chiamata `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### Completato il capitolo

* Chiamata `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### Salta nel capitolo

* Chiamata `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implement chapter tracking {#section_52221B3A9BFD46B3A22DA6BCE97CCD75}

1. Identify when the chapter start event occurs and create the `ChapterObject` instance by using the chapter information.

   Here is the `ChapterObject` chapter tracking reference:

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
1. To begin tracking the chapter playback, call the `ChapterStart` event in the `MediaHeartbeat` instance.
1. When playback reaches the chapter end boundary, as defined by your custom code, call the `ChapterComplete` event in the `MediaHeartbeat` instance.
1. If chapter playback did not complete because the user chose to skip the chapter (for example, if the user seeks out of the chapter boundary), call the `ChapterSkip` event in the MediaHeartbeat instance.
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

## Validate {#section_07EC2811BE3249249494596BFE9BF869}

### Inizio capitolo

All'avvio di una riproduzione di un capitolo, viene inviata una chiamata di chiave:

* Inizio del capitolo Heartbeat (questa chiamata contiene ulteriori variabili di metadati capitolo).

### Completamento capitolo

Al termine del capitolo, viene inviato un capitolo Heartbeat complete.

### Ignora capitolo

Quando un capitolo viene ignorato, viene inviata una chiamata di ignora dei capitoli Heartbeat.
