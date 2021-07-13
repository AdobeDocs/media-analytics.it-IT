---
title: Scopri come tenere traccia degli annunci su Android
description: Implementa il tracciamento degli annunci nelle applicazioni Android tramite Media SDK.
uuid: 4a4249fb-dc39-4947-a14d-a51d972f32d4
exl-id: 1f96dde9-c924-4fce-8b14-7dec7137f265
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 6%

---

# Tracciamento annunci su Android{#track-ads-on-android}

>[!IMPORTANT]
>
>Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione tramite gli SDK 2.x. Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

## Costanti di tracciamento degli annunci

| Nome costante | Descrizione |
| --- | --- |
| `MediaHeartbeat.Event.AdBreakStart` | Costante per il tracciamento dell&#39;evento di avvio AdBreak |
| `MediaHeartbeat.Event.AdBreakComplete` | Costante per il tracciamento dell’evento AdBreak Complete |
| `MediaHeartbeat.Event.AdStart` | Costante per il tracciamento dell’evento Ad Start |
| `MediaHeartbeat.Event.AdComplete` | Costante per il tracciamento dell’evento Ad Complete |
| `MediaHeartbeat.Event.AdSkip` | Costante per il tracciamento dell’evento Ad Skip |

## Passaggi di implementazione

1. Identifica quando inizia il limite di interruzione dell&#39;annuncio, incluso il pre-roll, e crea un `AdBreakObject` utilizzando le informazioni di interruzione dell&#39;annuncio.

   `AdBreakObject` riferimento:

   | Nome variable | Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `name` | Nome dell’interruzione dell’annuncio come pre-roll, mid-roll e post-roll. | Sì |
   | `position` | La posizione numerica dell’interruzione pubblicitaria all’interno del contenuto, a partire da 1. | Sì |
   | `startTime` | Valore della testina di riproduzione all&#39;inizio dell&#39;interruzione pubblicitaria. | Sì |

   Creazione dell’oggetto di interruzione annuncio:

   ```java
   MediaObject adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Invoca `trackEvent()` con `AdBreakStart` nell&#39;istanza `MediaHeartbeat` per iniziare a tracciare l&#39;interruzione pubblicitaria:

   ```java
   public void onAdBreakStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,  
                             adBreakInfo,  
                             null); 
   }
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

   ```java
   MediaObject adInfo =  
     MediaHeartbeat.createAdObject(<AD_NAME> 
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Facoltativamente, allega metadati standard e/o di annunci alla sessione di tracciamento dei contenuti multimediali tramite variabili di dati di contesto.

   * [Implementazione dei metadati standard di annunci su Android](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
   * **Metadati di annunci personalizzati -** Per i metadati personalizzati, crea un oggetto variabile per le variabili di dati personalizzate e compila i dati per l&#39;annuncio corrente:

      ```java
      // Setting Ad Metadata 
      HashMap<String, String> adMetadata = new HashMap<String, String>(); 
      adMetadata.put("affiliate", "Sample affiliate"); 
      adMetadata.put("campaign", "Sample ad campaign");
      ```

1. Chiama `trackEvent()` con l&#39;evento `AdStart` nell&#39;istanza `MediaHeartbeat` per iniziare a tracciare la riproduzione dell&#39;annuncio.

   Includi un riferimento alla variabile di metadati personalizzata (o a un oggetto vuoto) come terzo parametro nella chiamata dell&#39;evento:

   ```java
   public void onAdStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                             adInfo,  
                             adMetadata); 
   }
   ```

1. Quando la riproduzione dell’annuncio raggiunge la fine dell’annuncio, invoca `trackEvent()` con l’evento `AdComplete` :

   ```java
   public void onAdComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
   }
   ```

1. Se la riproduzione dell&#39;annuncio non è stata completata perché l&#39;utente ha scelto di saltare l&#39;annuncio, tieni traccia dell&#39;evento `AdSkip`:

   ```java
   public void onAdSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdSkip, null, null); 
   }
   ```

1. Se sono presenti annunci aggiuntivi all&#39;interno dello stesso `AdBreak`, ripeti nuovamente i passaggi da 3 a 7.
1. Al termine dell’interruzione pubblicitaria, utilizza l’evento `AdBreakComplete` per tenere traccia di:

   ```java
   public void onAdBreakComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
   }
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con annunci pre-scorrimento](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) .
