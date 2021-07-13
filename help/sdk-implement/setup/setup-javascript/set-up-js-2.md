---
title: Come impostare Media SDK con JavaScript 2.x
description: Segui questi passaggi per configurare l’applicazione Media SDK su JavaScript 2.x.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
exl-id: 33976096-8b86-4353-906b-e25bf4693471
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 6%

---

# Configurazione JavaScript 2.x{#set-up-javascript}

## Prerequisiti

* **Ottieni**
parametri di configurazione validiQuesti parametri possono essere ottenuti da un rappresentante di Adobe dopo aver configurato il tuo account di analisi.
* **Implementazione  `AppMeasurement` di JavaScript nell&#39;**
applicazione multimedialePer ulteriori informazioni sull&#39;SDK di Adobe Mobile, consulta  [Implementazione di Analytics utilizzando JavaScript.](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=it)

* **Fornisci le seguenti funzionalità nel lettore multimediale:**

   * *Un’API per abbonarti agli eventi*  del lettore: l’SDK per contenuti multimediali richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.
   * *API che fornisce informazioni*  sul lettore. Queste informazioni includono dettagli quali il nome del contenuto multimediale e la posizione della testina di riproduzione.

1. Aggiungi la libreria [scaricata](/help/sdk-implement/download-sdks.md#download-2x-sdks) al tuo progetto. Crea riferimenti locali alle classi per comodità.

   1. Espandi il file `MediaSDK-js-v2.*.zip` scaricato.
   1. Verifica che il file `MediaSDK.min.js` esista nella directory `libs`:

   1. Ospita il file `MediaSDK.min.js` .

      Questo file JavaScript di base deve essere ospitato su un server web accessibile a tutte le pagine del sito. È necessario il percorso di questi file per il passaggio successivo.

   1. Fate riferimento a `MediaSDK.min.js` su tutte le pagine del sito.

      Includi `MediaSDK` per JavaScript aggiungendo la seguente riga di codice nel tag `<head>` o `<body>` in ogni pagina. Ad esempio:

      ```
      <script type="text/javascript"
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. Per verificare rapidamente che la libreria sia stata importata correttamente, crea un&#39;istanza della classe `ADB.va.MediaHeartbeatConfig` .

      >[!NOTE]
      >
      >Dalla versione 2.1.0, l’SDK JavaScript è conforme alle specifiche dei moduli AMD e CommonJS e `VideoHeartbeat.min.js` può essere utilizzato anche con caricatori di moduli compatibili.

1. Per un facile accesso alle API, crea riferimenti locali alle classi `MediaHeartbeat` .

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   ```

1. Crea un&#39;istanza `MediaHeartbeatConfig`.

   Questa sezione ti aiuta a comprendere i parametri di configurazione `MediaHeartbeat` e come impostare i valori di configurazione corretti sull&#39;istanza `MediaHeartbeat` per un monitoraggio accurato.

   Esempio di inizializzazione `MediaHeartbeatConfig`:

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

1. Implementa il protocollo `MediaHeartbeatDelegate` .

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

1. Crea l&#39;istanza `MediaHeartbeat` .

   Utilizza i valori `MediaHeartbeatConfig` e `MediaHeartbeatDelegate` per creare l&#39;istanza `MediaHeartbeat`.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Assicurati che l&#39;istanza `MediaHeartbeat` sia accessibile e non venga deallocata fino alla fine della sessione multimediale. Questa istanza verrà utilizzata per tutti i seguenti eventi di tracciamento.

   >[!TIP]
   >
   >`MediaHeartbeat` richiede un&#39;istanza di  `AppMeasurement` per inviare chiamate ad Adobe Analytics. Ecco un esempio di istanza `AppMeasurement`:

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   appMeasurement.account = <rsid>;
   appMeasurement.pageName = <page_name>;
   appMeasurement.charSet = "UTF­8";
   ```

## Migrare da JavaScript 1.x a 2.x

Nella versione 2.x, tutti i metodi pubblici sono consolidati nella classe `ADB.va.MediaHeartbeat` per facilitare gli sviluppatori. Inoltre, tutte le configurazioni sono ora consolidate nella classe `ADB.va.MediaHeartbeatConfig` .

Per informazioni dettagliate sulla migrazione da 1.x a 2.x, consulta [Migrazione da VHL 1.x a 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
