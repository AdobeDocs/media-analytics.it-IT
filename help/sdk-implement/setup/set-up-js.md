---
seo-title: Configurare JavaScript
title: Configurare JavaScript
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Configurare JavaScript{#set-up-javascript}

## Prerequisiti

* **Ottenete parametri** di configurazione validi Questi parametri possono essere ottenuti da un rappresentante Adobe dopo aver configurato l'account di analisi.
* **Implementazione`AppMeasurement`di JavaScript nell’applicazione** multimediale. Per ulteriori informazioni sulla documentazione SDK di Adobe Mobile, consulta [Implementazione di Analytics tramite JavaScript.](https://marketing.adobe.com/resources/help/en_US/sc/implement/js_implementation.html)

* **Fornite le seguenti funzionalità nel lettore multimediale:**

   * *Un'API per iscriversi agli eventi* del lettore - L'SDK di Media richiede che venga chiamato un set di API semplici quando si verificano eventi nel lettore.
   * *API che fornisce informazioni* sul lettore - Queste informazioni includono dettagli quali il nome del supporto e la posizione della testina di riproduzione.

1. Aggiungete la libreria [scaricata](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) al progetto. Create riferimenti locali alle classi per comodità.

   1. Espandete il `MediaSDK-js-v2.*.zip` file scaricato.
   1. Verificate che il `MediaSDK.min.js` file esista nella `libs` directory:

   1. Ospita il `MediaSDK.min.js` file.

      Questo file JavaScript di base deve essere ospitato su un server Web accessibile a tutte le pagine del sito. È necessario che il percorso di questi file venga completato nel passaggio successivo.

   1. Fate riferimento a `MediaSDK.min.js` su tutte le pagine del sito.

      Include `MediaSDK` for JavaScript by adding the following line of code in the `<head>` or `<body>` tag on each page. Ad esempio:

      ```
      <script type="text/javascript" 
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. Per verificare rapidamente che la libreria sia stata importata correttamente, create un'istanza della `ADB.va.MediaHeartbeatConfig` classe.

      >[!NOTE]
      >
      >Dalla versione 2.1.0, l’SDK JavaScript è conforme alle specifiche dei moduli AMD e CommonJS e `VideoHeartbeat.min.js` può essere utilizzato anche con caricatori di moduli compatibili.

1. Per un accesso facilitato alle API, create riferimenti locali alle `MediaHeartbeat` classi.

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   ```

1. Create un' `MediaHeartbeatConfig` istanza.

   Questa sezione descrive i parametri di `MediaHeartbeat` configurazione e come impostare i valori di configurazione corretti nell’ `MediaHeartbeat` istanza, per un monitoraggio accurato.

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

1. Implementa il `MediaHeartbeatDelegate` protocollo.

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

1. Create l’ `MediaHeartbeat` istanza.

   Utilizzate l'icona `MediaHeartbeatConfig` e `MediaHeartbeatDelegate` per creare l' `MediaHeartbeat` istanza.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Accertatevi che l’ `MediaHeartbeat` istanza sia accessibile e non venga deallocata fino alla fine della sessione multimediale. Questa istanza verrà utilizzata per tutti i seguenti eventi di tracciamento.

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

## Migrazione dalla versione 1.x alla 2.x in JavaScript

Nella versione 2.x, tutti i metodi pubblici sono consolidati nella `ADB.va.MediaHeartbeat` classe per semplificare gli sviluppatori. Inoltre, tutte le configurazioni sono ora consolidate nella `ADB.va.MediaHeartbeatConfig` classe.

Per informazioni dettagliate sulla migrazione da 1.x a 2.x, consultate Migrazione [VHL 1.x a 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
