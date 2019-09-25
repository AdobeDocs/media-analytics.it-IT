---
seo-title: Panoramica
title: Panoramica
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Panoramica{#overview}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione mediante gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

La riproduzione di annunci include il tracciamento di interruzioni di annunci, avvii di annunci, completamenti di annunci e salti di annunci. Utilizzate l'API del lettore multimediale per identificare gli eventi del lettore chiave e per compilare le variabili di annuncio richieste e facoltative. Consultate l'elenco completo dei metadati qui: Parametri [annuncio.](/help/metrics-and-metadata/ad-parameters.md)

## Eventi del lettore {#player-events}


### Attivazione e interruzione

>[!NOTE]
>Incluso il pre-roll

* Create un'istanza di `adBreak` oggetto per l'interruzione annuncio. Ad esempio, `adBreakObject`.

* Chiama `trackEvent` per iniziare la pausa pubblicitaria con il tuo `adBreakObject`.

### Per ogni avvio della risorsa annuncio

* Create un'istanza di oggetto annuncio per la risorsa annuncio. Ad esempio, `adObject`.
* Compilate i metadati dell'annuncio, `adCustomMetadata`.
* Chiama `trackEvent` l'inizio dell'annuncio.

### Per ogni annuncio completato

* Chiamata `trackEvent` per l'annuncio completo.

### Attivato annuncio

* Chiama `trackEvent` il salto dell'annuncio.

### Al termine dell'interruzione dell'annuncio

* Chiamata `trackEvent` per l'interruzione dell'annuncio completata.

## Implementazione del tracciamento degli annunci {#section_83E0F9406A7743E3B57405D4CDA66F68}

### Costanti di tracciamento annunci

| Nome costante | Descrizione   |
|---|---|
| `AdBreakStart` | Costante per il tracciamento dell'evento AdBreak Start |
| `AdBreakComplete` | Costante per il tracciamento dell'evento AdBreak Complete |
| `AdStart` | Costante per il tracciamento dell'evento Ad Start |
| `AdComplete` | Costante per il tracciamento dell'evento Ad Complete |
| `AdSkip` | Costante per il tracciamento dell'evento Ad Skip |

### Passaggi di implementazione

1. Identificate quando inizia il limite di interruzione annuncio, incluso il pre-roll, e create un'interruzione `AdBreakObject` utilizzando le informazioni di interruzione annuncio.

   `AdBreakObject` riferimento:

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome dell’interruzione dell’annuncio come pre-roll, mid-roll e post-roll. | Sì |
   | `position` | La posizione numerica dell'interruzione annuncio all'interno del contenuto, a partire da 1. | Sì |
   | `startTime` | Valore dell'indicatore di riproduzione all'inizio dell'interruzione dell'annuncio. | Sì |

1. Chiama `trackEvent()` con `AdBreakStart` nell’ `MediaHeartbeat` istanza per iniziare a monitorare l’interruzione dell’annuncio.

1. Identificare quando inizia l'annuncio e creare un' `AdObject` istanza utilizzando le informazioni sull'annuncio.

   `AdObject` riferimento:

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome descrittivo dell'annuncio. | Sì |
   | `adId` | Identificatore univoco per l’annuncio. | Sì |
   | `position` | La posizione del numero dell'annuncio all'interno dell'interruzione dell'annuncio, a partire da 1. | Sì |
   | `length` | Lunghezza annuncio | Sì |

1. Se necessario, allegate metadati standard e/o di annunci alla sessione di tracciamento tramite variabili di dati di contesto.

   * **Metadati annuncio standard - Per metadati annuncio standard,** create un dizionario di coppie di valori di metadati di annunci standard utilizzando le chiavi per la vostra piattaforma.
   * **Custom ad metadata -** Per i metadati personalizzati, create un oggetto variabile per le variabili di dati personalizzate e inserite i dati per l'annuncio corrente.

1. Chiamate `trackEvent()` con l’ `AdStart` evento nell’ `MediaHeartbeat` istanza per iniziare a monitorare la riproduzione dell’annuncio.

   Includete un riferimento alla variabile di metadati personalizzata (o a un oggetto vuoto) come terzo parametro nella chiamata dell’evento.

1. Quando la riproduzione dell’annuncio raggiunge la fine dell’annuncio, invoca `trackEvent()` con l’ `AdComplete` evento.

1. Se la riproduzione dell'annuncio non è stata completata perché l'utente ha scelto di saltare l'annuncio, tracciate l' `AdSkip` evento.
1. Se ci sono altri annunci all'interno dello stesso `AdBreak`, ripeti di nuovo i passaggi da 3 a 7.
1. Al termine dell'interruzione dell'annuncio, utilizzate l' `AdBreakComplete` evento per tracciarlo.

>[!IMPORTANT]
>
>Accertatevi di NON incrementare la testina di riproduzione del lettore di contenuti (`l:event:playhead`) durante la riproduzione dell'annuncio (`s:asset:type=ad`). In questo caso, le metriche Content Time Spent (Tempo contenuto trascorso) avranno un impatto negativo.

Il codice di esempio seguente utilizza l’SDK JavaScript 2.x per un lettore multimediale HTML5.

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

