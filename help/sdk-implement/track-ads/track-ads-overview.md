---
seo-title: Panoramica
title: Panoramica
uuid: 1607798 b-c 6 ef -4 d 60-8 e 40-e 958 c 345 b 09 c
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Panoramica{#overview}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione tramite gli SDK 2. x. Se implementhi una versione 1. x dell'SDK, puoi scaricare le guide per sviluppatori 1. x qui: [Scarica gli SDK.](/help/sdk-implement/download-sdks.md)

La riproduzione di annunci include interruzioni di annunci pubblicitari, avvii annunci, annunci pubblicitari e annunci. Utilizzate l'API del lettore multimediale per identificare gli eventi del lettore chiave e compilare le variabili pubblicitarie richieste e facoltative. Consultate l'elenco completo dei metadati qui: [Parametri annuncio.](/help/metrics-and-metadata/ad-parameters.md)

## Eventi del lettore {#player-events}


### All'avvio di un annuncio

>[!NOTE]
>Inclusione di prerelease

* Creare un'istanza `adBreak` di oggetto per l'interruzione di annuncio. Ad esempio, `adBreakObject`.

* Invoca l `trackEvent` 'interruzione di annuncio con il tuo `adBreakObject`.

### In ogni avvio di risorse pubblicitarie

* Create un'istanza di oggetto annuncio per la risorsa pubblicitaria. Ad esempio, `adObject`.
* Compilare i metadati `adCustomMetadata`degli annunci,
* Richiedi `trackEvent` l'avvio dell'annuncio.

### Per ogni annuncio completo

* Call `trackEvent` for the ad complete.

### On jump

* Chiamata `trackEvent` per l'ad skip.

### All'interruzione di annunci

* Chiamata `trackEvent` per l'interruzione di annuncio.

## Implementare il tracciamento degli annunci {#section_83E0F9406A7743E3B57405D4CDA66F68}

### Costanti di tracciamento annunci

| Nome costante | Descrizione   |
|---|---|
| `AdBreakStart` | Costante per il tracciamento dell'evento adbreak Start |
| `AdBreakComplete` | Costante per il tracciamento dell'evento adbreak Complete |
| `AdStart` | Costante per il tracciamento dell'evento Ad Start |
| `AdComplete` | Costante per il tracciamento dell'evento Ad Complete |
| `AdSkip` | Costante per il tracciamento dell'evento Ad Skip |

### Passaggi di implementazione

1. Identifica l'inizio del confine dell'interruzione di annunci, incluso l'pre-roll, e crea un' `AdBreakObject` immagine utilizzando le informazioni sull'interruzione di annunci.

   `AdBreakObject` riferimento:

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome dell'interruzione pubblicitaria, ad esempio pre-roll, mid-roll e post-roll. | Sì |
   | `position` | La posizione numerica dell'interruzione di annunci all'interno del contenuto, a partire da 1. | Sì |
   | `startTime` | Valore della linea di scansione all'inizio dell'interruzione di annuncio. | Sì |

1. Chiama `trackEvent()` con `AdBreakStart` nell `MediaHeartbeat` 'istanza per iniziare a tracciare l'interruzione di annuncio.

1. Identifica l'avvio dell'annuncio e crea un `AdObject` 'istanza utilizzando le informazioni sull'annuncio.

   `AdObject` riferimento:

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome descrittivo dell'annuncio. | Sì |
   | `adId` | Identificatore univoco dell'annuncio. | Sì |
   | `position` | La posizione numerica dell'annuncio nell'interruzione di annuncio, a partire da 1. | Sì |
   | `length` | Lunghezza annuncio | Sì |

1. Se necessario, allega metadati standard e/o annuncio alla sessione di tracciamento attraverso variabili di dati contestuali.

   * **Metadati degli annunci standard -** Per i metadati degli annunci standard, create un dizionario di coppie di valori chiave per metadati pubblicitari standard utilizzando le chiavi per la piattaforma.
   * **Custom annunmetadati:** per i metadati personalizzati, crea un oggetto variabile per le variabili dati personalizzate e popolate i dati per l'annuncio corrente.

1. Chiama `trackEvent()` con l' `AdStart` evento nell `MediaHeartbeat` 'istanza per iniziare a tracciare la riproduzione degli annunci.

   Includete un riferimento alla variabile di metadati personalizzata (o un oggetto vuoto) come terzo parametro nella chiamata dell'evento.

1. Quando la riproduzione dell'annuncio raggiunge la fine dell'annuncio, chiama `trackEvent()` con l' `AdComplete` evento.

1. Se la riproduzione degli annunci non è stata completata perché l'utente ha scelto di ignorare l'annuncio, tieni traccia dell' `AdSkip` evento.
1. Se vi sono annunci aggiuntivi nello stesso `AdBreak`modo, ripetete i passaggi da 3 a 7.
1. Al termine dell'interruzione di annuncio, utilizzate l' `AdBreakComplete` evento per tracciarlo.

>[!IMPORTANT]
>
>Accertatevi di NON incrementare l'indicatore di riproduzione del lettore di contenuto (`l:event:playhead`) durante la riproduzione ad annuncio (`s:asset:type=ad`). In caso contrario, le metriche Tempo contenuto risulteranno compromesse.

Il seguente codice di esempio utilizza l'SDK javascript 2. x per un lettore multimediale HTML 5.

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

