---
title: Configurare JavaScript 3.x
description: Configurazione dell’applicazione Media SDK per l’implementazione in JavaScript 3.x.
translation-type: tm+mt
source-git-commit: b642bd1a136e62901847f2a8cf004d05282fca01
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 5%

---


# Configurare JavaScript 3.x{#set-up-javascript}

## Prerequisiti

* **Ottenete parametri** di configurazione validi Questi parametri possono essere ottenuti da un rappresentante Adobe dopo aver configurato l&#39;account di analisi.
* **Implementazione`AppMeasurement`e`Experience Cloud Identity Service`per JavaScript nell&#39;applicazione** multimediale. Per ulteriori informazioni, consulta [Implementazione di Analytics tramite JavaScript](https://docs.adobe.com/content/help/it-IT/analytics/implementation/js/overview.html) e [Implementazione di Experience Cloud Identity Service.](https://docs.adobe.com/content/help/en/id-service/using/implementation/setup-analytics.html)

* **Fornite le seguenti funzionalità nel lettore multimediale:**

   * *Un&#39;API per iscriversi agli eventi* del lettore - L&#39;SDK di Media richiede che venga chiamato un set di API semplici quando si verificano eventi nel lettore.
   * *Un&#39;API che fornisce informazioni* sul lettore, che include informazioni sui contenuti multimediali, annunci pubblicitari e capitoli attualmente in fase di riproduzione.

1. Aggiungete la libreria [scaricata](/help/sdk-implement/download-sdks.md#download-3x-sdks) al progetto. Create riferimenti locali alle classi per comodità.

   1. Espandete il `MediaSDK-js-v3*.zip` file scaricato.
   1. Verificate che il `MediaSDK.js` file esista nella `libs` directory.

   1. Ospita il `MediaSDK.js` file.

      Questo file JavaScript di base deve essere ospitato su un server Web accessibile a tutte le pagine del sito. È necessario che il percorso di questi file venga completato nel passaggio successivo.

   1. Fate riferimento a `MediaSDK.js` su tutte le pagine del sito.

      Include `MediaSDK` for JavaScript by adding the following line of code in the `<head>` or `<body>` tag on each page. Ad esempio:

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. Per verificare rapidamente che la libreria sia stata importata correttamente, verificare `ADB.Media` è stato esportato sull&#39;oggetto Window.

      >[!NOTE]
      >
      >L’SDK JavaScript è conforme alle specifiche dei moduli AMD e CommonJS e `MediaSDK.js` può essere utilizzato anche con caricatori di moduli compatibili.

1. Create un&#39;istanza di `AppMeasurement` e configurate `visitor`.

   La configurazione di Media SDK richiede un&#39;istanza di `AppMeasurement` con `visitor` configurazione.

   ```js
    var appMeasurement = new AppMeasurement(“<rsid>”);
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = “<visitor_namespace>.sc.omtrdc.net”;
   ```

1. Configurare Media SDK

   Media SDK deve essere configurato una volta per ogni pagina Web e la configurazione si applica a tutte le istanze di tracciamento create.

   >[!IMPORTANT]
   >
   > Media SDK (3.x) utilizza l&#39;API di Media Collection per tenere traccia dei supporti, che è diverso dall&#39;endpoint HB utilizzato negli SDK 2.x. Per ulteriori informazioni, contattate il rappresentante Adobe.

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

1. Create l’ `MediaTracker` istanza.

   Dopo aver configurato Media SDK, è possibile creare istanze di tracciamento per tenere traccia del contenuto multimediale tramite `getInstance` API.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >Accertatevi che l’ `tracker` istanza sia accessibile e non venga deallocata fino alla fine della sessione multimediale. Questa istanza verrà utilizzata per tenere traccia di tutti gli eventi seguenti per la sessione.

## Migrazione da JavaScript 2.x a 3.x

Per informazioni dettagliate sulla migrazione da 2.x a 3.x, consultate Migrazione da [2.x a 3.x.](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)
