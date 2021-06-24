---
title: Scopri come tenere traccia degli annunci utilizzando JavaScript 2.x
description: Implementa il tracciamento degli annunci nelle applicazioni browser (JS) utilizzando Media SDK.
uuid: 4d81d29c-c55d-4d48-b505-3260922712ff
exl-id: 4404d3a6-ab98-40f0-9573-ee32f480f650
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 6%

---

# Tracciare gli annunci utilizzando JavaScript 2.x{#track-ads-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione tramite gli SDK 2.x. Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento degli annunci

| Nome costante | Descrizione   |
|---|---|
| `AdBreakStart` | Costante per il tracciamento dell&#39;evento di avvio AdBreak |
| `AdBreakComplete` | Costante per il tracciamento dell’evento AdBreak Complete |
| `AdStart` | Costante per il tracciamento dell’evento Ad Start |
| `AdComplete` | Costante per il tracciamento dell’evento Ad Complete |
| `AdSkip` | Costante per il tracciamento dell’evento Ad Skip |

## Passaggi di implementazione

1. Identifica quando inizia il limite di interruzione dell&#39;annuncio, incluso il pre-roll, e crea un `AdBreakObject` utilizzando le informazioni di interruzione dell&#39;annuncio.

   `AdBreakObject` riferimento:

   | Nome variable | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome dell’interruzione dell’annuncio come pre-roll, mid-roll e post-roll. | Sì |
   | `position` | La posizione numerica dell’interruzione pubblicitaria che inizia con 1. | Sì |
   | `startTime` | Valore della testina di riproduzione all&#39;inizio dell&#39;interruzione pubblicitaria. | Sì |

   Creazione dell’oggetto di interruzione annuncio:

   ```js
   var adBreakObject =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Invoca `trackEvent()` con `AdBreakStart` nell&#39;istanza `MediaHeartbeat` per iniziare a tracciare l&#39;interruzione pubblicitaria:

   ```js
   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
   ```

1. Identifica quando l&#39;annuncio inizia e crea un&#39;istanza `AdObject` utilizzando le informazioni dell&#39;annuncio.

   `AdObject` riferimento:

   | Nome variable | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome descrittivo dell&#39;annuncio. | Sì |
   | `adId` | Identificatore univoco per l&#39;annuncio. | Sì |
   | `position` | La posizione numerica dell’annuncio all’interno dell’interruzione pubblicitaria, a partire da 1. | Sì |
   | `length` | Lunghezza annuncio | Sì |

   Creazione di oggetti annuncio:

   ```js
   var adObject =  
     MediaHeartbeat.createAdObject(<AD_NAME>,  
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Facoltativamente, allega metadati standard e/o di annunci alla sessione di tracciamento dei contenuti multimediali tramite variabili di dati di contesto.

   * [Implementazione dei metadati standard di annunci in JavaScript](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
   * **Metadati di annunci personalizzati -** Per i metadati personalizzati, crea un oggetto variabile per le variabili di dati personalizzate e compila i dati per l&#39;annuncio corrente:

      ```js
      /* Set custom context data */
      var adCustomMetadata = {
          affiliate: "Sample affiliate",
          campaign: "Sample ad campaign",
          creative: "Sample creative"
      };
      ```

1. Chiama `trackEvent()` con l&#39;evento `AdStart` nell&#39;istanza `MediaHeartbeat` per iniziare a tracciare la riproduzione dell&#39;annuncio.

   Includi un riferimento alla variabile di metadati personalizzata (o a un oggetto vuoto) come terzo parametro nella chiamata dell&#39;evento:

   ```js
   _onAdStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                                       adObject,  
                                       adCustomMetadata);
   };
   ```

1. Quando la riproduzione dell’annuncio raggiunge la fine dell’annuncio, invoca `trackEvent()` con l’evento `AdComplete` :

   ```js
   _onAdComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
   };
   ```

1. Se la riproduzione dell&#39;annuncio non è stata completata perché l&#39;utente ha scelto di saltare l&#39;annuncio, tieni traccia dell&#39;evento `AdSkip`:

   ```js
   _onAdSkip = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
   };
   ```

1. Se sono presenti annunci aggiuntivi all&#39;interno dello stesso `AdBreak`, ripeti nuovamente i passaggi da 3 a 7.
1. Al termine dell’interruzione pubblicitaria, utilizza l’evento `AdBreakComplete` per tenere traccia di:

   ```js
   _onAdBreakComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
   };
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con annunci pre-scorrimento](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) .
