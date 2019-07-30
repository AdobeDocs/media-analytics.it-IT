---
seo-title: Configurare javascript
title: Configurare javascript
uuid: 0269 d 8 ad -0 af 8-4 bf 1-9 d 15-e 06 c 2952 a 005
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Set up JavaScript{#set-up-javascript}

## Prerequisiti

* **Ottenete parametri
di configurazione validi** Questi parametri possono essere ottenuti da un rappresentante Adobe dopo aver configurato il vostro account Analytics.
* **Implementazione`AppMeasurement`per javascript nell'applicazione
multimediale** Per ulteriori informazioni sulla documentazione SDK di Adobe Mobile, consulta [Implementazione di analisi tramite javascript.](https://marketing.adobe.com/resources/help/en_US/sc/implement/js_implementation.html)

* **Fornite le seguenti funzionalità nel lettore multimediale:**

   * *API per l'iscrizione agli eventi del lettore* - L'SDK di Media richiede che venga chiamato un set di API semplici quando si verificano eventi nel lettore.
   * *API che fornisce informazioni* sul lettore: informazioni dettagliate quali il nome del supporto e la posizione della testina di riproduzione.

1. Add your [downloaded](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) library to your project. Creare riferimenti locali alle classi per comodità.

   1. Expand the `MediaSDK-js-v2.*.zip` file that you downloaded.
   1. Verify that the `MediaSDK.min.js` file exists in the `libs` directory:

   1. Host the `MediaSDK.min.js` file.

      Questo file javascript di base deve essere ospitato su un server Web accessibile a tutte le pagine del sito. È necessario definire il percorso di questi file per il passaggio successivo.

   1. Fate riferimento a `MediaSDK.min.js` su tutte le pagine del sito.

      Include `MediaSDK` for JavaScript by adding the following line of code in the `<head>` or `<body>` tag on each page. Ad esempio:

      ```
      <script type="text/javascript" 
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. To quickly verify that the library was successfully imported, instantiate the `ADB.va.MediaHeartbeatConfig` class.

      >[!NOTE]
      >
      >From Version 2.1.0, the JavaScript SDK is compliant with the AMD and CommonJS module specifications, and `VideoHeartbeat.min.js` can also be used with compatible module loaders.

1. For easy access to the APIs, create local references to the `MediaHeartbeat` classes.

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   ```

1. Create a `MediaHeartbeatConfig` instance.

   This section helps you to understand `MediaHeartbeat` config parameters and how to set correct config values on your `MediaHeartbeat` instance, for accurate tracking.

   Esempio `MediaHeartbeatConfig` di inizializzazione:

   ```js
   //Media Heartbeat initialization 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER; 
   mediaConfig.playerName = Configuration.PLAYER.NAME; 
   mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL; 
   mediaConfig.debugLogging = true; 
   mediaConfig.appVersion = Configuration.HEARTBEAT.SDK; 
   mediaConfig.ssl = false; 
   mediaConfig.ovp = Configuration.HEARTBEAT.OVP; 
   ```

1. Implement the `MediaHeartbeatDelegate` protocol.

   ```js
   var mediaDelegate = new MediaHeartbeatDelegate(); 
   
   // Replace <currentPlaybackTime> with the video player current playback time 
   mediaDelegate.getCurrentPlaybackTime = function() { 
       return <currentPlaybackTime>; 
   }; 
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.  
   mediaDelegate.getQoSObject = function() { 
       return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>); 
   };
   ```

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` and `MediaHeartbeatDelegate` to create the `MediaHeartbeat` instance.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the media session. Questa istanza verrà utilizzata per tutti i seguenti eventi di tracciamento.

   >[!TIP]
   >
   >`MediaHeartbeat` richiede un'istanza di `AppMeasurement` invio di chiamate ad Adobe Analytics. Here is an example of an `AppMeasurement` instance:

   ```js
   var appMeasurement = new AppMeasurement(); 
   appMeasurement.visitor = visitor; 
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net"; 
   appMeasurement.account = <rsid>; 
   appMeasurement.pageName = <page_name>; 
   appMeasurement.charSet = "UTF­8";
   ```

## Migrazione dalla versione 1. x alla 2. x in javascript

In version 2.x, all of the public methods are consolidated into the `ADB.va.MediaHeartbeat` class to make it easier on developers. Also, all configs are now consolidated into the `ADB.va.MediaHeartbeatConfig` class.

For detailed information about migrating from 1.x to 2.x, see [VHL 1.x to 2.x Migration.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
