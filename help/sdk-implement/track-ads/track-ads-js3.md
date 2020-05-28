---
title: Tracciare gli annunci tramite JavaScript 3.x
description: Implementa il tracciamento degli annunci nelle applicazioni del browser (JS) tramite Media SDK.
translation-type: tm+mt
source-git-commit: f5b3961e0525c26b682490a4376d244c2703ae24
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 4%

---


# Tracciare gli annunci tramite JavaScript 3.x{#track-ads-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione mediante gli SDK 3.x. Se stai implementando versioni precedenti dell’SDK, puoi scaricare le Guide per gli sviluppatori qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

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

   | Nome della variabile | Tipo | Descrizione |
   | --- | --- | --- |
   | `name` | string | Stringa non vuota che denota il nome dell&#39;interruzione adattiva (pre-roll, mid-roll e post-roll). |
   | `position` | number | La posizione del numero dell&#39;interruzione annuncio che inizia con 1. |
   | `startTime` | number | Valore dell&#39;indicatore di riproduzione all&#39;inizio dell&#39;interruzione dell&#39;annuncio. |

   Creazione oggetto di interruzione annuncio:

   ```js
   var adBreakObject =
     ADB.Media.createAdBreakObject(<ADBREAK_NAME>,
                                      <POSITION>,
                                      <START_TIME>);
   ```

1. Chiama `trackEvent()` con `AdBreakStart` nell’ `MediaHeartbeat` istanza per iniziare a monitorare l’interruzione dell’annuncio:

   ```js
   tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);
   ```

1. Identificare quando inizia l&#39;annuncio e creare un&#39; `AdObject` istanza utilizzando le informazioni sull&#39;annuncio.

   `AdObject` riferimento:

   | Nome della variabile | Tipo | Descrizione |
   | --- | --- | --- |
   | `name` | string | Stringa non vuota che denota il nome dell&#39;annuncio. |
   | `adId` | string | Stringa non vuota che denota un identificatore di annuncio. |
   | `position` | number | La posizione del numero dell&#39;annuncio all&#39;interno dell&#39;interruzione iniziale, iniziando da 1. |
   | `length` | number | Numero positivo che indica la lunghezza dell’annuncio. |

   Creazione di oggetti annuncio:

   ```js
   var adObject =
     ADB.Media.createAdObject.createAdObject(<AD_NAME>,
                                   <AD_ID>,
                                   <POSITION>,
                                   <LENGTH>);
   ```

1. Se necessario, allegate metadati standard e/o di annunci alla sessione di tracciamento dei supporti tramite le variabili dei dati contestuali.

   * [Implementazione dei metadati standard di annunci in JavaScript](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-js.md)
   * **Metadati annunci personalizzati -** Per i metadati personalizzati, create un oggetto variabile per le variabili dati personalizzate e compilate con i dati per l&#39;annuncio corrente:

      ```js
      /* Set context data */
      // Standard metadata keys provided by adobe.
      adMetadata[ADB.Media.AdMetadataKeys.ADVERTISER]  ="Sample Advertiser";
      adMetadata[ADB.Media.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
      
      // Custom metadata keys
      adMetadata["affiliate"] = "Sample affiliate";
      adMetadata["campaign"] = "Sample ad campaign";
      adMetadata["creative"] = "Sample creative";
      ```

1. Chiamate `trackEvent()` con l’ `AdStart` evento nell’ `MediaHeartbeat` istanza per iniziare a monitorare la riproduzione dell’annuncio.

   Includete un riferimento alla variabile di metadati personalizzata (o a un oggetto vuoto) come terzo parametro nella chiamata dell’evento:

   ```js
   _onAdStart = function() {
       tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
   };
   ```

1. Quando la riproduzione dell’annuncio raggiunge la fine dell’annuncio, invoca `trackEvent()` con l’ `AdComplete` evento:

   ```js
   _onAdComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdComplete);
   };
   ```

1. Se la riproduzione dell&#39;annuncio non è stata completata perché l&#39;utente ha scelto di saltare l&#39;annuncio, tieni traccia dell&#39; `AdSkip` evento:

   ```js
   _onAdSkip = function() {
       tracker.trackEvent(ADB.Media.Event.AdSkip);
   };
   ```

1. Se ci sono altri annunci all&#39;interno dello stesso `AdBreak`, ripeti di nuovo i passaggi da 3 a 7.
1. Al termine dell&#39;interruzione dell&#39;annuncio, utilizzate l&#39; `AdBreakComplete` evento per tenere traccia:

   ```js
   _onAdBreakComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
   };
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento della riproduzione [VOD con annunci](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) pre-roll.
