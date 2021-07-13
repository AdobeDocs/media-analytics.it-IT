---
title: Come impostare Media SDK con JavaScript 3.x
description: Segui questi passaggi per configurare l’applicazione Media SDK su JavaScript 3.x.
exl-id: 35e27495-e480-4463-9f00-4b60a54d02c1
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 6%

---

# Configurazione JavaScript 3.x{#set-up-javascript}

## Prerequisiti

* **Ottieni**
parametri di configurazione validiQuesti parametri possono essere ottenuti da un rappresentante di Adobe dopo aver configurato il tuo account di analisi.
* **Implementazione  `AppMeasurement` e  `Experience Cloud Identity Service` per JavaScript nell’**
applicazione multimedialePer ulteriori informazioni, consulta  [Implementazione di Analytics con ](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=it) JavaScript e  [Implementazione del servizio Experience Cloud Identity](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html).

* **Fornisci le seguenti funzionalità nel lettore multimediale:**

   * *Un’API per abbonarti agli eventi*  del lettore: l’SDK per contenuti multimediali richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.
   * *API che fornisce informazioni*  sul lettore, incluse informazioni sulla riproduzione di contenuti multimediali, annunci pubblicitari e capitoli.

1. Aggiungi la libreria [scaricata](/help/sdk-implement/download-sdks.md#download-3x-sdks) al tuo progetto. Crea riferimenti locali alle classi per comodità.

   1. Espandi il file `MediaSDK-js-v3*.zip` scaricato.
   1. Verifica che il file `MediaSDK.js` esista nella directory `libs`.

   1. Ospita il file `MediaSDK.js` .

      Questo file JavaScript di base deve essere ospitato su un server web accessibile a tutte le pagine del sito. È necessario il percorso di questi file per il passaggio successivo.

   1. Fate riferimento a `MediaSDK.js` su tutte le pagine del sito.

      Includi `MediaSDK` per JavaScript aggiungendo la seguente riga di codice nel tag `<head>` o `<body>` in ogni pagina. Ad esempio:

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. Per verificare rapidamente che la libreria sia stata importata correttamente, controlla che `ADB.Media` sia esportato sull&#39;oggetto Window.

      >[!NOTE]
      >
      >L’SDK JavaScript è conforme alle specifiche dei moduli AMD e CommonJS e può essere utilizzato `MediaSDK.js` anche con caricatori di moduli compatibili.

1. Crea un&#39;istanza di `AppMeasurement` e configura `visitor`.

   La configurazione Media SDK richiede un&#39;istanza di `AppMeasurement` con `visitor` configurato.

   ```js
    var appMeasurement = new AppMeasurement(“<rsid>”);
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = “<visitor_namespace>.sc.omtrdc.net”;
   ```

1. Configurare Media SDK

   Media SDK deve essere configurato una volta per pagina web e la configurazione si applica a tutte le istanze di tracciamento create.

   >[!IMPORTANT]
   >
   > Media SDK (3.x) utilizza l’API di raccolta multimediale per il tracciamento dei contenuti multimediali che è diverso dall’endpoint HB utilizzato negli SDK 2.x. Per ulteriori informazioni, contatta il tuo rappresentante di Adobe.

   Esempio di inizializzazione `MediaConfig`:

   ```js
    // Create MediaConfig object (same as above)
    var mediaConfig = new ADB.MediaConfig();
    mediaConfig.trackingServer = Configuration.MEDIA_COLLECTION_ENDPOINT;
    mediaConfig.playerName = Configuration.PLAYER_NAME;
    mediaConfig.channel = Configuration.CHANNEL;
    mediaConfig.appVersion = Configuration.APP_VERSION;
    mediaConfig.debugLogging = false;
    mediaConfig.ssl = true;
   
    ADB.Media.configure(mediaConfig, appMeasurement);
   ```

1. Crea l&#39;istanza `MediaTracker` .

   Dopo aver configurato Media SDK, le istanze di tracciamento per il tracciamento del contenuto multimediale possono essere create utilizzando `getInstance` API.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >Assicurati che l&#39;istanza `tracker` sia accessibile e non venga deallocata fino alla fine della sessione multimediale. Questa istanza verrà utilizzata per monitorare tutti gli eventi seguenti per quella sessione.

## Migrare da JavaScript 2.x a 3.x

Per informazioni dettagliate sulla migrazione da 2.x a 3.x, consulta [2.x a 3.x Migration.](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)
