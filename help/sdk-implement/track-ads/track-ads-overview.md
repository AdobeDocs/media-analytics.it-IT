---
title: Spiegazione di Track Ads
description: Panoramica dell’implementazione del tracciamento degli annunci con Media SDK.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 4%

---

# Panoramica{#overview}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione tramite gli SDK 2.x. Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

La riproduzione degli annunci include il tracciamento delle interruzioni degli annunci, gli avvii degli annunci, i completamenti degli annunci e gli annunci salti. Utilizza l’API del lettore multimediale per identificare gli eventi del lettore chiave e popolare le variabili di annuncio richieste e facoltative. Vedi l&#39;elenco completo dei metadati qui: [Parametri annuncio.](/help/metrics-and-metadata/ad-parameters.md)

## Eventi del lettore {#player-events}


### All&#39;avvio dell&#39;interruzione dell&#39;annuncio

>[!NOTE]
>Incluso pre-roll

* Crea un&#39;istanza di oggetto `adBreak` per l&#39;interruzione pubblicitaria. Ad esempio, `adBreakObject`.

* Chiama `trackEvent` per iniziare l&#39;interruzione dell&#39;annuncio con il tuo `adBreakObject`.

### A ogni avvio di risorse pubblicitarie

* Crea un&#39;istanza di oggetto annuncio per la risorsa annuncio. Ad esempio, `adObject`.
* Compila i metadati dell’annuncio, `adCustomMetadata`.
* Chiama `trackEvent` per l&#39;inizio dell&#39;annuncio.

### A ogni annuncio completato

* Chiama `trackEvent` per completare l&#39;annuncio.

### On ad salto

* Chiama `trackEvent` per il salto dell&#39;annuncio.

### Interruzione annuncio completata

* Chiama `trackEvent` per completare l&#39;interruzione pubblicitaria.

## Implementare il tracciamento degli annunci {#implement-ad-tracking}

### Costanti di tracciamento degli annunci

| Nome costante | Descrizione   |
|---|---|
| `AdBreakStart` | Costante per il tracciamento dell&#39;evento di avvio AdBreak |
| `AdBreakComplete` | Costante per il tracciamento dell’evento AdBreak Complete |
| `AdStart` | Costante per il tracciamento dell’evento Ad Start |
| `AdComplete` | Costante per il tracciamento dell’evento Ad Complete |
| `AdSkip` | Costante per il tracciamento dell’evento Ad Skip |

### Passaggi di implementazione

1. Identifica quando inizia il limite di interruzione dell&#39;annuncio, incluso il pre-roll, e crea un `AdBreakObject` utilizzando le informazioni di interruzione dell&#39;annuncio.

   `AdBreakObject` riferimento:

   | Nome variable | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome dell’interruzione dell’annuncio come pre-roll, mid-roll e post-roll. | Sì |
   | `position` | La posizione numerica dell’interruzione pubblicitaria all’interno del contenuto, a partire da 1. | Sì |
   | `startTime` | Valore della testina di riproduzione all&#39;inizio dell&#39;interruzione pubblicitaria. | Sì |

1. Chiama `trackEvent()` con `AdBreakStart` nell&#39;istanza `MediaHeartbeat` per iniziare a tracciare l&#39;interruzione pubblicitaria.

1. Identifica quando l&#39;annuncio inizia e crea un&#39;istanza `AdObject` utilizzando le informazioni dell&#39;annuncio.

   `AdObject` riferimento:

   | Nome variable | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome descrittivo dell&#39;annuncio. | Sì |
   | `adId` | Identificatore univoco per l&#39;annuncio. | Sì |
   | `position` | La posizione numerica dell’annuncio all’interno dell’interruzione pubblicitaria, a partire da 1. | Sì |
   | `length` | Lunghezza annuncio | Sì |

1. Facoltativamente, allega metadati standard e/o di annunci alla sessione di tracciamento tramite variabili di dati di contesto.

   * **Metadati degli annunci standard:** per i metadati standard di annunci, crea un dizionario di coppie di valori chiave degli annunci standard utilizzando le chiavi per la piattaforma.
   * **Metadati di annunci personalizzati -** Per i metadati personalizzati, crea un oggetto variabile per le variabili di dati personalizzate e compila i dati per l’annuncio corrente.

1. Chiama `trackEvent()` con l&#39;evento `AdStart` nell&#39;istanza `MediaHeartbeat` per iniziare a tracciare la riproduzione dell&#39;annuncio.

   Includi un riferimento alla variabile di metadati personalizzata (o a un oggetto vuoto) come terzo parametro nella chiamata dell&#39;evento.

1. Quando la riproduzione dell’annuncio raggiunge la fine dell’annuncio, invoca `trackEvent()` con l’evento `AdComplete` .

1. Se la riproduzione dell&#39;annuncio non è stata completata perché l&#39;utente ha scelto di saltare l&#39;annuncio, tieni traccia dell&#39;evento `AdSkip` .
1. Se sono presenti annunci aggiuntivi all&#39;interno dello stesso `AdBreak`, ripeti nuovamente i passaggi da 3 a 7.
1. Al termine dell’interruzione pubblicitaria, utilizza l’evento `AdBreakComplete` per tracciarlo.

>[!IMPORTANT]
>
>Assicurati di NON incrementare la testina di riproduzione del lettore di contenuti (`l:event:playhead`) durante la riproduzione dell&#39;annuncio (`s:asset:type=ad`). In questo caso, le metriche Content Time Spent (Tempo contenuto trascorso) saranno influenzate negativamente.

Il codice di esempio seguente utilizza l&#39;SDK JavaScript 2.x per un lettore multimediale HTML5.

```js
/* Call on ad break start */ 
 
if (e.type == "ad break start") { 
    var adBreakObject = MediaHeartbeat.createAdBreakObject("mid-roll", 2, 500); 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject); 
}; 
 
/* Call on ad start */ 
if (e.type == "ad start") { 
    var adObject = MediaHeartbeat.createAdObject("PepsiOne", "123456ab", 1, 30); 
    /* Set custom context data */ 
    var adCustomMetadata = { 
        affiliate:"Sample affiliate", 
        campaign:"Sample ad campaign", 
        creative:"Sample creative" 
    } 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata); 
}; 
 
/* Call on ad complete */ 
if (e.type == "ad complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
}; 
 
/* Call on ad skip */ 
if (e.type == "ad skip") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
}; 
     
/* Call on ad break complete */ 
if (e.type == "ad break complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
}; 
```
