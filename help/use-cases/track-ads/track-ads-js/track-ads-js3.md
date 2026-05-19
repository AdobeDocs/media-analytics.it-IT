---
title: Scopri come tracciare gli annunci utilizzando JavaScript 3.x
description: Implementa il tracciamento degli annunci nelle applicazioni browser (JS) utilizzando l’SDK per contenuti multimediali.
exl-id: 6b34b2c0-5e50-471a-b52c-b9c760fa3169
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/j8xAr1QwslwoGu5IKvW14wFjyCSMMIIerA1t-JECNcQ
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 406
ht-degree: 88%

---

# Tracciare gli annunci utilizzando JavaScript 3.x{#track-ads-on-javascript}

Le istruzioni seguenti forniscono indicazioni per l’implementazione utilizzando gli SDK 3.x.

>[!IMPORTANT]
>
>Se implementi una versione precedente dell’SDK, puoi scaricare le Guide per sviluppatori qui: [Scaricare gli SDK.](/help/getting-started/download-sdks.md)

## Costanti di tracciamento degli annunci

| Nome costante | Descrizione   |
|---|---|
| `AdBreakStart` | Costante per il tracciamento dell’evento di avvio AdBreak |
| `AdBreakComplete` | Costante per il tracciamento dell’evento AdBreak Complete |
| `AdStart` | Costante per il tracciamento dell’evento Ad Start |
| `AdComplete` | Costante per il tracciamento dell’evento Ad Complete |
| `AdSkip` | Costante per il tracciamento dell’evento Ad Skip |

## Passaggi di implementazione

1. Identifica quando inizia il limite dell’interruzione dell’annuncio, incluso il pre-roll, e crea un `AdBreakObject` utilizzando le informazioni sull’interruzione dell’annuncio.

   Specifihe di `AdBreakObject`:

   | Nome variabile | Tipo | Descrizione |
   | --- | --- | --- |
   | `name` | string | Stringa non vuota che denota il nome dell’interruzione (pre-roll, mid-roll e post-roll). |
   | `position` | numero | La posizione numerica dell’interruzione pubblicitaria che inizia con 1. |
   | `startTime` | numero | Valore della testina di riproduzione all’inizio dell’interruzione pubblicitaria. |

   Creazione dell’oggetto di interruzione annuncio:

   ```js
   var adBreakObject =
     ADB.Media.createAdBreakObject(<ADBREAK_NAME>,
                                      <POSITION>,
                                      <START_TIME>);
   ```

1. Chiamata `trackEvent()` con `AdBreakStart` nell’istanza `MediaHeartbeat` per iniziare a tracciare l’interruzione pubblicitaria:

   ```js
   tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);
   ```

1. Identifica quando inizia l’annuncio e crea un’istanza `AdObject` utilizzando le informazioni sull’annuncio.

   Specifihe di `AdObject`:

   | Nome variabile | Tipo | Descrizione |
   | --- | --- | --- |
   | `name` | string | Stringa non vuota che denota il nome dell’annuncio. |
   | `adId` | string | Stringa non vuota che denota l’identificatore dell’annuncio. |
   | `position` | numero | La posizione numerica dell’annuncio all’interno dell’interruzione, partendo da 1. |
   | `length` | numero | Numero positivo che indica la lunghezza dell’annuncio. |

   Creazione di oggetti annuncio:

   ```js
   var adObject =
     ADB.Media.createAdObject.createAdObject(<AD_NAME>,
                                   <AD_ID>,
                                   <POSITION>,
                                   <LENGTH>);
   ```

1. (Facoltativo) Allega metadati standard e/o di annunci alla sessione di tracciamento dei contenuti multimediali tramite variabili di dati di contesto.

   * [Implementazione dei metadati standard di annunci in JavaScript](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
   * **Metadati degli annunci personalizzati -** Per i metadati personalizzati, crea un oggetto variabile per le variabili di dati personalizzate e compila i dati per l’annuncio corrente:

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

1. Chiamata `trackEvent()` con l’evento `AdStart` nell’istanza `MediaHeartbeat` per iniziare a tracciare la riproduzione dell’annuncio.

   Includi un riferimento alla variabile di metadati personalizzata (o a un oggetto vuoto) come terzo parametro nella chiamata dell’evento:

   ```js
   _onAdStart = function() {
       tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
   };
   ```

1. Quando la riproduzione dell’annuncio raggiunge la fine dell’annuncio, chiama `trackEvent()` con l’evento `AdComplete`:

   ```js
   _onAdComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdComplete);
   };
   ```

1. Se la riproduzione dell’annuncio non è stata completata perché l’utente ha scelto di saltare l’annuncio, tieni traccia dell’evento `AdSkip`:

   ```js
   _onAdSkip = function() {
       tracker.trackEvent(ADB.Media.Event.AdSkip);
   };
   ```

1. Se ci sono annunci aggiuntivi all’interno dello stesso `AdBreak`, ripeti di nuovo i passaggi da 3 a 7.
1. Al termine dell’interruzione pubblicitaria, utilizza l’evento `AdBreakComplete` per tracciare:

   ```js
   _onAdBreakComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
   };
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con annunci pre-roll](/help/use-cases/tracking-scenarios/vod-preroll-ads.md).

## Tracciamento granulare degli annunci

L&#39;intervallo di ping predefinito dell&#39;annuncio è `10 seconds`.

È possibile impostare il tracciamento granulare degli annunci per abilitare il tracciamento degli annunci `1 second`.

>[!IMPORTANT]
>
>Queste informazioni devono essere fornite all’avvio di una sessione di tracciamento.



**Sintassi**

```javascript
ADB.Media.MediaObjectKey = {
   GranularAdTracking: "media.granularadtracking"
   }
```

**Esempio**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

// Enable granular ad tracking
mediaObject[ADB.Media.MediaObjectKey.GranularAdTracking] = true;

tracker.trackSessionStart(mediaObject);
```
