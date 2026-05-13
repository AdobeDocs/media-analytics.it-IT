---
title: Scopri come tracciare gli annunci in iOS
description: Implementa il tracciamento degli annunci nelle applicazioni iOS tramite Media SDK.
uuid: e979e679-cde5-4c30-8f34-867feceac13a
exl-id: a352bca9-bcfc-4418-b2a2-c9b1ad226359
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/4z8fq-mojLd4zzlCJsZQ7R7AOc5W59x0u-yOTpylojc
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 367
ht-degree: 100%

---

# Tracciare gli annunci su iOS{#track-ads-on-ios}

Le istruzioni seguenti forniscono indicazioni per l’implementazione tramite gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell’SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/getting-started/download-sdks.md)

## Costanti di tracciamento degli annunci

| Nome costante | Descrizione   |
|---|---|
| `ADBMediaHeartbeatEventAdBreakStart` | Costante per il tracciamento dell’evento di avvio AdBreak |
| `ADBMediaHeartbeatEventAdBreakComplete` | Costante per il tracciamento dell’evento AdBreak Complete |
| `ADBMediaHeartbeatEventAdStart` | Costante per il tracciamento dell’evento Ad Start |
| `ADBMediaHeartbeatEventAdComplete` | Costante per il tracciamento dell’evento Ad Complete |
| `ADBMediaHeartbeatEventAdSkip` | Costante per il tracciamento dell’evento Ad Skip |

## Passaggi di implementazione

1. Identifica quando inizia il limite dell’interruzione dell’annuncio, incluso il pre-roll, e crea un `AdBreakObject` utilizzando le informazioni sull’interruzione dell’annuncio.

   Specifihe di `AdBreakObject`:

   | Nome variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome dell’interruzione dell’annuncio come pre-roll, mid-roll e post-roll. | Sì |
   | `position` | La posizione numerica dell’interruzione pubblicitaria all’interno del contenuto, a partire da 1. | Sì |
   | `startTime` | Valore della testina di riproduzione all’inizio dell’interruzione pubblicitaria. | Sì |

   Creazione dell’oggetto di interruzione annuncio:

   ```
   id adBreakObject = [ADBMediaHeartbeat createAdBreakObjectWithName:[ADBREAK_NAME]
                               position:[POSITION]  
                               startTime:[START_TIME]];
   ```

1. Chiamata `trackEvent()` con `AdBreakStart` nell’istanza `MediaHeartbeat` per iniziare a tracciare l’interruzione pubblicitaria:

   ```
   - (void)onAdBreakStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                        mediaObject:adBreakObject  
                        data:nil];
   }
   ```

1. Identifica quando inizia l’annuncio e crea un’istanza `AdObject` utilizzando le informazioni sull’annuncio.

   Specifihe di `AdObject`:

   | Nome variabile | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome descrittivo dell’annuncio. | Sì |
   | `adId` | Identificatore univoco per l’annuncio. | Sì |
   | `position` | La posizione numerica dell’annuncio all’interno dell’interruzione pubblicitaria, a partire da 1. | Sì |
   | `length` | Lunghezza annuncio | Sì |

   Creazione di oggetti annuncio:

   ```
   id adObject = [ADBMediaHeartbeat createAdObjectWithName:[AD_NAME]
                                    adId:[AD_ID]
                                    position:[POSITION]
                                    length:[LENGTH]];
   ```

1. Facoltativamente, allega metadati standard e/o di annunci alla sessione di tracciamento dei contenuti multimediali tramite variabili di dati di contesto.

   * [Implementare metadati standard di annunci su iOS](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
   * **Metadati degli annunci personalizzati -** Per i metadati personalizzati, crea un oggetto variabile per le variabili di dati personalizzate e compila i dati per l’annuncio corrente:

     ```
     NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init];
     [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"];
     [adDictionary setObject:@"Sample campaign" forKey:@"campaign"];
     [adDictionary setObject:@"Sample creative" forKey:@"creative"];
     ```

1. Chiamata `trackEvent()` con l’evento `AdStart` nell’istanza `MediaHeartbeat` per iniziare a tracciare la riproduzione dell’annuncio.

   Includi un riferimento alla variabile di metadati personalizzata (o a un oggetto vuoto) come terzo parametro nella chiamata dell’evento:

   ```
   - (void)onAdStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                        mediaObject:adObject  
                        data:adDictionary];
   }
   ```

1. Quando la riproduzione dell’annuncio ne raggiunge la fine, esegui la chiamata `trackEvent()` con l’evento `AdComplete`.

   ```
   - (void)onAdComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. Se la riproduzione dell’annuncio non è stata completata perché l’utente ha scelto di saltarlo, traccia l’evento `AdSkip`.

   ```
   - (void)onAdSkip:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdSkip  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. Se ci sono annunci aggiuntivi all’interno dello stesso `AdBreak`, ripeti di nuovo i passaggi da 3 a 7.
1. Al termine dell’interruzione pubblicitaria, utilizza l’evento `AdBreakComplete` per tracciare:

   ```
   - (void)onAdBreakComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con annunci pre-roll](/help/use-cases/tracking-scenarios/vod-preroll-ads.md).
