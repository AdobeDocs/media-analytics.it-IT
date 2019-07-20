---
seo-title: Tenere traccia degli annunci in javascript
title: Tenere traccia degli annunci in javascript
uuid: 4 d 81 d 29 c-c 55 d -4 d 48-b 505-3260922712 ff
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Track ads on JavaScript{#track-ads-on-javascript}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione tramite gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

## Costanti di tracciamento annunci

| Nome costante | Descrizione   |
|---|---|
| `AdBreakStart` | Costante per il tracciamento dell'evento adbreak Start |
| `AdBreakComplete` | Costante per il tracciamento dell'evento adbreak Complete |
| `AdStart` | Costante per il tracciamento dell'evento Ad Start |
| `AdComplete` | Costante per il tracciamento dell'evento Ad Complete |
| `AdSkip` | Costante per il tracciamento dell'evento Ad Skip |

## Passaggi di implementazione

1. Identify when the ad break boundary begins, including pre-roll, and create an `AdBreakObject` by using the ad break information.

   `AdBreakObject` riferimento:

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome dell'interruzione pubblicitaria, ad esempio pre-roll, mid-roll e post-roll. | Sì |
   | `position` | La posizione numerica dell'interruzione di annuncio a partire da 1. | Sì |
   | `startTime` | Valore della linea di scansione all'inizio dell'interruzione di annuncio. | Sì |

   Creazione di oggetti per analisi annunci:

   ```js
   var adBreakObject =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break:

   ```js
   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
   ```

1. Identify when the ad starts and create an `AdObject` instance using the ad information.

   `AdObject` riferimento:

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome descrittivo dell'annuncio. | Sì |
   | `adId` | Identificatore univoco dell'annuncio. | Sì |
   | `position` | La posizione numerica dell'annuncio nell'interruzione di annuncio, a partire da 1. | Sì |
   | `length` | Lunghezza annuncio | Sì |

   Creazione di oggetti ad:

   ```js
   var adObject =  
     MediaHeartbeat.createAdObject(<AD_NAME>,  
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Se necessario, allega metadati standard e/o annuncio alla sessione di tracciamento multimediale attraverso le variabili di dati di contesto.

   * [Implementare i metadati degli annunci standard in javascript](../../sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-js.md)
   * **Custom annunmetadati:** per i metadati personalizzati, crea un oggetto variabile per le variabili dati personalizzate e popolate i dati per l'annuncio corrente:

      ```js
      /* Set custom context data */ 
      var adCustomMetadata = { 
          affiliate: "Sample affiliate", 
          campaign: "Sample ad campaign", 
          creative: "Sample creative" 
      };
      ```

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   Includete un riferimento alla variabile di metadati personalizzata (o un oggetto vuoto) come terzo parametro nella chiamata dell'evento:

   ```js
   _onAdStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                                       adObject,  
                                       adCustomMetadata); 
   };
   ```

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event:

   ```js
   _onAdComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
   };
   ```

1. If ad playback did not complete because the user chose to skip the ad, track the `AdSkip` event:

   ```js
   _onAdSkip = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
   };
   ```

1. If there are any additional ads within the same `AdBreak`, repeat steps 3 through 7 again.
1. When the ad break is complete, use the `AdBreakComplete` event to track:

   ```js
   _onAdBreakComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
   };
   ```

See the tracking scenario [VOD playback with pre-roll ads](../../sdk-implement/tracking-scenarios/vod-preroll-ads.md) for more information.
