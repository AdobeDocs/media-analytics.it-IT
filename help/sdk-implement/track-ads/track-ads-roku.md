---
title: Scopri come tenere traccia degli annunci su Roku
description: Implementa il tracciamento degli annunci nelle applicazioni Roku utilizzando Media SDK.
uuid: b1567265-7043-4efa-a313-aaaa91c4bb01
exl-id: aaed828d-1aba-486e-83e3-2ffd092305e2
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 5%

---

# Tracciamento annunci su Roku{#track-ads-on-roku}

Le istruzioni seguenti forniscono indicazioni per l&#39;implementazione tramite gli SDK 2.x.

>[!IMPORTANT]
>
>Se implementi una versione 1.x dell&#39;SDK, puoi scaricare le guide per sviluppatori 1.x qui: [Scaricare gli SDK.](/help/sdk-implement/download-sdks.md)

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

   ```
   ‘ Create an adbreak info object
   adBreakInfo = adb_media_init_adbreakinfo()
   adBreakInfo.name = <ADBREAK_NAME>
   adBreakInfo.startTime = <START_TIME>
   adBreakInfo.position = <POSITION>
   ```

1. Invoca `trackEvent()` con `AdBreakStart` nell&#39;istanza `MediaHeartbeat` per iniziare a tracciare l&#39;interruzione pubblicitaria:

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_START, adBreakInfo, contextData)
   ```

1. Identifica quando inizia la risorsa dell’annuncio e crea un’istanza `AdObject` utilizzando le informazioni dell’annuncio.

   ```
   adInfo =  
     adb_media_init_adinfo(ad.title,  
                           ad.id,  
                           ad.position,  
                           ad.duration)
   ```

1. Facoltativamente, allega metadati standard e/o di annunci alla sessione di tracciamento dei contenuti multimediali tramite variabili di dati di contesto.

   * [Implementazione dei metadati standard di annunci su Roku](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   * **Metadati annuncio personalizzati:** per i metadati personalizzati, crea un oggetto variabile per le variabili di dati personalizzate e compila i dati per la risorsa annuncio corrente:

      ```
      contextData = {}
      contextData["adinfo1"] = "adinfo2"
      contextData["adinfo2"] = "adinfo2"
      ```

1. Invoca `trackEvent()` con l&#39;evento `AdStart` nell&#39;istanza `MediaHeartbeat` per iniziare a tracciare la riproduzione dell&#39;annuncio:

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_START, adInfo, contextData)
   ```

1. Quando la riproduzione della risorsa dell’annuncio raggiunge la fine dell’annuncio, invoca `trackEvent()` con l’evento `AdComplete` .

   ```
   standardAdMetadata = {}
   contextData = {}
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_COMPLETE, adInfo, contextData)
   ```

1. Se la riproduzione dell&#39;annuncio non è stata completata perché l&#39;utente ha scelto di saltare l&#39;annuncio, tieni traccia dell&#39;evento `AdSkip`:

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_SKIP, adInfo, contextData
   ```

1. Se sono presenti annunci aggiuntivi all&#39;interno dello stesso `AdBreak`, ripeti nuovamente i passaggi da 3 a 7.
1. Al termine dell’interruzione pubblicitaria, utilizza l’evento `AdBreakComplete` per tenere traccia di:

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_COMPLETE, adBreakInfo, contextData)
   ```

Per ulteriori informazioni, consulta lo scenario di tracciamento [Riproduzione VOD con annunci pre-scorrimento](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) .
