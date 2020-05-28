---
title: Tracciare gli annunci tramite JavaScript 2.x
description: Implementa il tracciamento degli annunci nelle applicazioni del browser (JS) tramite Media SDK.
uuid: 4d81d29c-c55d-4d48-b505-3260922712ff
translation-type: tm+mt
source-git-commit: f5b3961e0525c26b682490a4376d244c2703ae24
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 6%

---


# Tracciare gli annunci tramite JavaScript 2.x{#track-ads-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione mediante gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento annunci

| Nome costante | Descrizione   |
|---|---|
| `AdBreakStart` | Costante per il tracciamento dell&#39;evento AdBreak Start |
| `AdBreakComplete` | Costante per il tracciamento dell&#39;evento AdBreak Complete |
| `AdStart` | Costante per il tracciamento dell&#39;evento Ad Start |
| `AdComplete` | Costante per il tracciamento dell&#39;evento Ad Complete |
| `AdSkip` | Costante per il tracciamento dell&#39;evento Ad Skip |

## Passaggi di implementazione

1. Identificate quando inizia il limite di interruzione annuncio, incluso il pre-roll, e create un&#39;interruzione `AdBreakObject` utilizzando le informazioni di interruzione annuncio.

   `AdBreakObject` riferimento:

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome dell’interruzione dell’annuncio come pre-roll, mid-roll e post-roll. | Sì |
   | `position` | La posizione del numero dell&#39;interruzione annuncio che inizia con 1. | Sì |
   | `startTime` | Valore dell&#39;indicatore di riproduzione all&#39;inizio dell&#39;interruzione dell&#39;annuncio. | Sì |

   Creazione oggetto di interruzione annuncio:

   ```js
   var adBreakObject =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Chiama `trackEvent()` con `AdBreakStart` nell’ `MediaHeartbeat` istanza per iniziare a monitorare l’interruzione dell’annuncio:

   ```js
   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
   ```

1. Identificare quando inizia l&#39;annuncio e creare un&#39; `AdObject` istanza utilizzando le informazioni sull&#39;annuncio.

   `AdObject` riferimento:

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome descrittivo dell&#39;annuncio. | Sì |
   | `adId` | Identificatore univoco per l’annuncio. | Sì |
   | `position` | La posizione del numero dell&#39;annuncio all&#39;interno dell&#39;interruzione dell&#39;annuncio, a partire da 1. | Sì |
   | `length` | Lunghezza annuncio | Sì |

   Creazione di oggetti annuncio:

   ```js
   var adObject =  
     MediaHeartbeat.createAdObject(<AD_NAME>,  
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Se necessario, allegate metadati standard e/o di annunci alla sessione di tracciamento dei supporti tramite le variabili dei dati contestuali.

   * [Implementazione dei metadati standard di annunci in JavaScript](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-js.md)
   * **Metadati annunci personalizzati -** Per i metadati personalizzati, create un oggetto variabile per le variabili dati personalizzate e compilate con i dati per l&#39;annuncio corrente:

      ```js
      /* Set custom context data */
      var adCustomMetadata = {
          affiliate: "Sample affiliate",
          campaign: "Sample ad campaign",
          creative: "Sample creative"
      };
      ```

1. Chiamate `trackEvent()` con l’ `AdStart` evento nell’ `MediaHeartbeat` istanza per iniziare a monitorare la riproduzione dell’annuncio.

   Includete un riferimento alla variabile di metadati personalizzata (o a un oggetto vuoto) come terzo parametro nella chiamata dell’evento:

   ```js
   _onAdStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                                       adObject,  
                                       adCustomMetadata);
   };
   ```

1. Quando la riproduzione dell’annuncio raggiunge la fine dell’annuncio, invoca `trackEvent()` con l’ `AdComplete` evento:

   ```js
   _onAdComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
   };
   ```

1. Se la riproduzione dell&#39;annuncio non è stata completata perché l&#39;utente ha scelto di saltare l&#39;annuncio, tieni traccia dell&#39; `AdSkip` evento:

   ```js
   _onAdSkip = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
   };
   ```

1. Se ci sono altri annunci all&#39;interno dello stesso `AdBreak`, ripeti di nuovo i passaggi da 3 a 7.
1. Al termine dell&#39;interruzione dell&#39;annuncio, utilizzate l&#39; `AdBreakComplete` evento per tenere traccia:

   ```js
   _onAdBreakComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
   };
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento della riproduzione [VOD con annunci](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) pre-roll.
