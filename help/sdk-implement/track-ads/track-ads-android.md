---
seo-title: Tracciare annunci su Android
title: Tracciare annunci su Android
uuid: 4 a 4249 fb-dc 39-4947-a 14 d-a 51 d 972 f 32 d 4
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Track ads on Android{#track-ads-on-android}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l'implementazione tramite gli SDK 2. x. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento annunci

| Nome costante | Descrizione |
| --- | --- |
| `MediaHeartbeat.Event.AdBreakStart` | Costante per il tracciamento dell'evento adbreak Start |
| `MediaHeartbeat.Event.AdBreakComplete` | Costante per il tracciamento dell'evento adbreak Complete |
| `MediaHeartbeat.Event.AdStart` | Costante per il tracciamento dell'evento Ad Start |
| `MediaHeartbeat.Event.AdComplete` | Costante per il tracciamento dell'evento Ad Complete |
| `MediaHeartbeat.Event.AdSkip` | Costante per il tracciamento dell'evento Ad Skip |

## Passaggi di implementazione

1. Identify when the ad break boundary begins, including pre-roll, and create an `AdBreakObject` by using the ad break information.

   `AdBreakObject` riferimento:

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome dell'interruzione pubblicitaria, ad esempio pre-roll, mid-roll e post-roll. | Sì |
   | `position` | La posizione numerica dell'interruzione di annunci all'interno del contenuto, a partire da 1. | Sì |
   | `startTime` | Valore della linea di scansione all'inizio dell'interruzione di annuncio. | Sì |

   Creazione di oggetti per analisi annunci:

   ```java
   MediaObject adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break:

   ```java
   public void onAdBreakStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,  
                             adBreakInfo,  
                             null); 
   }
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

   ```java
   MediaObject adInfo =  
     MediaHeartbeat.createAdObject(<AD_NAME> 
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Se necessario, allega metadati standard e/o annuncio alla sessione di tracciamento multimediale attraverso le variabili di dati di contesto.

   * [Implementare i metadati degli annunci standard su Android](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
   * **Custom annunmetadati:** per i metadati personalizzati, crea un oggetto variabile per le variabili dati personalizzate e popolate i dati per l'annuncio corrente:

      ```java
      // Setting Ad Metadata 
      HashMap<String, String> adMetadata = new HashMap<String, String>(); 
      adMetadata.put("affiliate", "Sample affiliate"); 
      adMetadata.put("campaign", "Sample ad campaign");
      ```

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   Includete un riferimento alla variabile di metadati personalizzata (o un oggetto vuoto) come terzo parametro nella chiamata dell'evento:

   ```java
   public void onAdStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                             adInfo,  
                             adMetadata); 
   }
   ```

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event:

   ```java
   public void onAdComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
   }
   ```

1. If ad playback did not complete because the user chose to skip the ad, track the `AdSkip` event:

   ```java
   public void onAdSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdSkip, null, null); 
   }
   ```

1. If there are any additional ads within the same `AdBreak`, repeat steps 3 through 7 again.
1. When the ad break is complete, use the `AdBreakComplete` event to track:

   ```java
   public void onAdBreakComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
   }
   ```

See the tracking scenario [VOD playback with pre-roll ads](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) for more information.
