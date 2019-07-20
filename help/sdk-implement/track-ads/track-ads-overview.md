---
seo-title: Panoramica
title: Panoramica
uuid: 1607798 b-c 6 ef -4 d 60-8 e 40-e 958 c 345 b 09 c
translation-type: tm+mt
source-git-commit: 56e8716ea37049b95a59a82144bbad0e882c16b4

---


# Panoramica{#overview}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione tramite gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

La riproduzione di annunci include interruzioni di annunci pubblicitari, avvii annunci, annunci pubblicitari e annunci. Utilizzate l'API del lettore multimediale per identificare gli eventi del lettore chiave e compilare le variabili pubblicitarie richieste e facoltative. See the comprehensive list of metadata here: [Ad parameters.](../../metrics-and-metadata/ad-parameters.md)

## Player events {#player-events}


### All'avvio di un annuncio

>[!NOTE]
>Inclusione di prerelease

* Create an `adBreak` object instance for the ad break. Ad esempio, `adBreakObject`.

* Call `trackEvent` for the ad break start with your `adBreakObject`.

### In ogni avvio di risorse pubblicitarie

* Create un'istanza di oggetto annuncio per la risorsa pubblicitaria. Ad esempio, `adObject`.
* Populate the ad metadata, `adCustomMetadata`.
* Call `trackEvent` for the ad start.

### Per ogni annuncio completo

* Call `trackEvent` for the ad complete.

### On jump

* Call `trackEvent` for the ad skip.

### All'interruzione di annunci

* Call `trackEvent` for the ad break complete.

## Implement ad tracking {#section_83E0F9406A7743E3B57405D4CDA66F68}

### Costanti di tracciamento annunci

| Nome costante | Descrizione   |
|---|---|
| `AdBreakStart` | Costante per il tracciamento dell'evento adbreak Start |
| `AdBreakComplete` | Costante per il tracciamento dell'evento adbreak Complete |
| `AdStart` | Costante per il tracciamento dell'evento Ad Start |
| `AdComplete` | Costante per il tracciamento dell'evento Ad Complete |
| `AdSkip` | Costante per il tracciamento dell'evento Ad Skip |

### Passaggi di implementazione

1. Identify when the ad break boundary begins, including pre-roll, and create an `AdBreakObject` by using the ad break information.

   `AdBreakObject` riferimento:

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome dell'interruzione pubblicitaria, ad esempio pre-roll, mid-roll e post-roll. | Sì |
   | `position` | La posizione numerica dell'interruzione di annunci all'interno del contenuto, a partire da 1. | Sì |
   | `startTime` | Valore della linea di scansione all'inizio dell'interruzione di annuncio. | Sì |

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break.

1. Identify when the ad starts and create an `AdObject` instance using the ad information.

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

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   Includete un riferimento alla variabile di metadati personalizzata (o un oggetto vuoto) come terzo parametro nella chiamata dell'evento.

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event.

1. If ad playback did not complete because the user chose to skip the ad, track the `AdSkip` event.
1. If there are any additional ads within the same `AdBreak`, repeat steps 3 through 7 again.
1. When the ad break is complete, use the `AdBreakComplete` event to track it.

>[!IMPORTANT]
>
>Make sure you do NOT increment the content player playhead (`l:event:playhead`) during ad playback (`s:asset:type=ad`). In caso contrario, le metriche Tempo contenuto risulteranno compromesse.

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

## Validate {#section_5F1783F5FE2644F1B94B0101F73D57EB}

### Inizio annuncio

All'avvio di una singola riproduzione, vengono inviate tre chiamate chiave nel seguente ordine:

1. Inizio analisi annunci video
1. Avvio heartbeat
1. Analytics Analytics start

Le chiamate 1 e 2 contengono ulteriori variabili di metadati sia per le versioni personalizzate che per quelle standard.

### Ad Play

Durante la riproduzione degli annunci, le chiamate a Heartbeat ad play vengono inviate al server Heartbeat ogni secondo.

### Annuncio completo

A 100% punti di un annuncio, verrà inviata una chiamata completa ad Heartbeat.

### Ad Skip

Quando un annuncio viene ignorato, non vengono inviati eventi, pertanto le chiamate di tracciamento non includeranno le informazioni sull'annuncio.

>[!TIP]
>
>Non viene inviata alcuna chiamata univoca all'avvio dell'interruzione di annunci e all'interruzione di annuncio.

