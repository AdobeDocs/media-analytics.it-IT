---
title: Scopri come tenere traccia degli annunci utilizzando JavaScript 3.x
description: Implementa il tracciamento degli annunci nelle applicazioni browser (JS) utilizzando Media SDK.
exl-id: 6b34b2c0-5e50-471a-b52c-b9c760fa3169
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 5%

---

# Tracciare gli annunci utilizzando JavaScript 3.x{#track-ads-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione tramite gli SDK 3.x. Se implementi una versione precedente dell’SDK, puoi scaricare le Guide per sviluppatori qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

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

   | Nome variable | Tipo | Descrizione |
   | --- | --- | --- |
   | `name` | string | Stringa non vuota che denota il nome dell’interruzione (pre-scorrimento, mid-roll e post-roll). |
   | `position` | numero | La posizione numerica dell’interruzione pubblicitaria che inizia con 1. |
   | `startTime` | numero | Valore della testina di riproduzione all&#39;inizio dell&#39;interruzione pubblicitaria. |

   Creazione dell’oggetto di interruzione annuncio:

   ```js
   var adBreakObject =
     ADB.Media.createAdBreakObject(<ADBREAK_NAME>,
                                      <POSITION>,
                                      <START_TIME>);
   ```

1. Invoca `trackEvent()` con `AdBreakStart` nell&#39;istanza `MediaHeartbeat` per iniziare a tracciare l&#39;interruzione pubblicitaria:

   ```js
   tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);
   ```

1. Identifica quando l&#39;annuncio inizia e crea un&#39;istanza `AdObject` utilizzando le informazioni dell&#39;annuncio.

   `AdObject` riferimento:

   | Nome variable | Tipo | Descrizione |
   | --- | --- | --- |
   | `name` | string | Stringa non vuota che denota il nome dell&#39;annuncio. |
   | `adId` | string | Stringa non vuota che denota l&#39;identificatore dell&#39;annuncio. |
   | `position` | numero | La posizione numerica dell’annuncio all’interno dell’interruzione di pagina, a partire da 1. |
   | `length` | numero | Numero positivo che indica la lunghezza dell’annuncio. |

   Creazione di oggetti annuncio:

   ```js
   var adObject =
     ADB.Media.createAdObject.createAdObject(<AD_NAME>,
                                   <AD_ID>,
                                   <POSITION>,
                                   <LENGTH>);
   ```

1. Facoltativamente, allega metadati standard e/o di annunci alla sessione di tracciamento dei contenuti multimediali tramite variabili di dati di contesto.

   * [Implementazione dei metadati standard di annunci in JavaScript](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
   * **Metadati di annunci personalizzati -** Per i metadati personalizzati, crea un oggetto variabile per le variabili di dati personalizzate e compila i dati per l&#39;annuncio corrente:

      ```js
      /* Set context data */
      // Standard metadata keys provided by adobe.
      adMetadata[ADB.Media.AdMetadataKeys]  ="Sample Advertiser";
      adMetadata[ADB.Media.AdMetadataKeys] = "Sample Campaign";
      
      // Custom metadata keys
      adMetadata["affiliate"] = "Sample affiliate";
      adMetadata["campaign"] = "Sample ad campaign";
      adMetadata["creative"] = "Sample creative";
      ```

1. Chiama `trackEvent()` con l&#39;evento `AdStart` nell&#39;istanza `MediaHeartbeat` per iniziare a tracciare la riproduzione dell&#39;annuncio.

   Includi un riferimento alla variabile di metadati personalizzata (o a un oggetto vuoto) come terzo parametro nella chiamata dell&#39;evento:

   ```js
   _onAdStart = function() {
       tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
   };
   ```

1. Quando la riproduzione dell’annuncio raggiunge la fine dell’annuncio, invoca `trackEvent()` con l’evento `AdComplete` :

   ```js
   _onAdComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdComplete);
   };
   ```

1. Se la riproduzione dell&#39;annuncio non è stata completata perché l&#39;utente ha scelto di saltare l&#39;annuncio, tieni traccia dell&#39;evento `AdSkip`:

   ```js
   _onAdSkip = function() {
       tracker.trackEvent(ADB.Media.Event.AdSkip);
   };
   ```

1. Se sono presenti annunci aggiuntivi all&#39;interno dello stesso `AdBreak`, ripeti nuovamente i passaggi da 3 a 7.
1. Al termine dell’interruzione pubblicitaria, utilizza l’evento `AdBreakComplete` per tenere traccia di:

   ```js
   _onAdBreakComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
   };
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con annunci pre-scorrimento](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) .
