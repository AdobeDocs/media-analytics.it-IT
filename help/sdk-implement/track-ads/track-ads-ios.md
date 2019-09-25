---
seo-title: Tracciare gli annunci su iOS
title: Tracciare gli annunci su iOS
uuid: e979e679-cde5-4c30-8f34-867feceac13a
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tracciare gli annunci su iOS{#track-ads-on-ios}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l’implementazione mediante gli SDK 2.x. Se stai implementando una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento annunci

| Nome costante | Descrizione   |
|---|---|
| `ADBMediaHeartbeatEventAdBreakStart` | Costante per il tracciamento dell'evento AdBreak Start |
| `ADBMediaHeartbeatEventAdBreakComplete` | Costante per il tracciamento dell'evento AdBreak Complete |
| `ADBMediaHeartbeatEventAdStart` | Costante per il tracciamento dell'evento Ad Start |
| `ADBMediaHeartbeatEventAdComplete` | Costante per il tracciamento dell'evento Ad Complete |
| `ADBMediaHeartbeatEventAdSkip` | Costante per il tracciamento dell'evento Ad Skip |

## Passaggi di implementazione

1. Identificate quando inizia il limite di interruzione annuncio, incluso il pre-roll, e create un'interruzione `AdBreakObject` utilizzando le informazioni di interruzione annuncio.

   `AdBreakObject` riferimento:

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome dell’interruzione dell’annuncio come pre-roll, mid-roll e post-roll. | Sì |
   | `position` | La posizione numerica dell'interruzione annuncio all'interno del contenuto, a partire da 1. | Sì |
   | `startTime` | Valore dell'indicatore di riproduzione all'inizio dell'interruzione dell'annuncio. | Sì |

   Creazione oggetto di interruzione annuncio:

   ```
   id adBreakObject = [ADBMediaHeartbeat createAdBreakObjectWithName:[ADBREAK_NAME] 
                               position:[POSITION]  
                               startTime:[START_TIME]];
   ```

1. Chiama `trackEvent()` con `AdBreakStart` nell’ `MediaHeartbeat` istanza per iniziare a monitorare l’interruzione dell’annuncio:

   ```
   - (void)onAdBreakStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                        mediaObject:adBreakObject  
                        data:nil]; 
   }
   ```

1. Identificare quando inizia l'annuncio e creare un' `AdObject` istanza utilizzando le informazioni sull'annuncio.

   `AdObject` riferimento:

   | Nome della variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome descrittivo dell'annuncio. | Sì |
   | `adId` | Identificatore univoco per l’annuncio. | Sì |
   | `position` | La posizione del numero dell'annuncio all'interno dell'interruzione dell'annuncio, a partire da 1. | Sì |
   | `length` | Lunghezza annuncio | Sì |

   Creazione di oggetti annuncio:

   ```
   id adObject = [ADBMediaHeartbeat createAdObjectWithName:[AD_NAME] 
                                    adId:[AD_ID] 
                                    position:[POSITION] 
                                    length:[LENGTH]];
   ```

1. Se necessario, allegate metadati standard e/o di annunci alla sessione di tracciamento dei supporti tramite le variabili dei dati contestuali.

   * [Implementazione di metadati di annunci standard su iOS](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
   * **Metadati annunci personalizzati -** Per i metadati personalizzati, create un oggetto variabile per le variabili dati personalizzate e compilate con i dati per l'annuncio corrente:

      ```
      NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init]; 
      [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"]; 
      [adDictionary setObject:@"Sample campaign" forKey:@"campaign"]; 
      [adDictionary setObject:@"Sample creative" forKey:@"creative"];
      ```

1. Chiamate `trackEvent()` con l’ `AdStart` evento nell’ `MediaHeartbeat` istanza per iniziare a monitorare la riproduzione dell’annuncio.

   Includete un riferimento alla variabile di metadati personalizzata (o a un oggetto vuoto) come terzo parametro nella chiamata dell’evento:

   ```
   - (void)onAdStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                        mediaObject:adObject  
                        data:adDictionary]; 
   }
   ```

1. Quando la riproduzione dell’annuncio raggiunge la fine dell’annuncio, invoca `trackEvent()` con l’ `AdComplete` evento.

   ```
   - (void)onAdComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Se la riproduzione dell'annuncio non è stata completata perché l'utente ha scelto di saltare l'annuncio, tracciate l' `AdSkip` evento.

   ```
   - (void)onAdSkip:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdSkip  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Se ci sono altri annunci all'interno dello stesso `AdBreak`, ripeti di nuovo i passaggi da 3 a 7.
1. Al termine dell'interruzione dell'annuncio, utilizzate l' `AdBreakComplete` evento per tenere traccia:

   ```
   - (void)onAdBreakComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento della riproduzione [VOD con annunci](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) pre-roll.
