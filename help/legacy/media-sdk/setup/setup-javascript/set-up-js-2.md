---
title: Configurare Media SDK con JavaScript 2.x
description: Segui questi passaggi per configurare l’applicazione Media SDK su JavaScript 2.x.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
exl-id: 33976096-8b86-4353-906b-e25bf4693471
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/mYfKt95xUE59MuMFOzGro6fPsJsdy4wcy2F2J--JaW8
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 408
ht-degree: 89%

---

# Configurare JavaScript 2.x{#set-up-javascript}

## Prerequisiti

* **Ottieni parametri di configurazione validi**
Questi parametri possono essere ottenuti da un rappresentante di Adobe dopo la configurazione dell’account di analisi.
* **Implementa `AppMeasurement` per JavaScript nell&#39;applicazione multimediale**
Per ulteriori informazioni sulla documentazione di Adobe Mobile SDK, vedi [Implementazione di Analytics con JavaScript.](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=it)

* **Fornisci le seguenti funzionalità nel lettore multimediale:**

   * *API per abbonarsi agli eventi del lettore*: Media SDK richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.
   * *API che fornisce informazioni sul lettore* - Queste informazioni includono dettagli quali il nome del supporto e la posizione della testina di riproduzione.

1. Aggiungi la libreria [scaricata](/help/getting-started/download-sdks.md) al progetto. Crea riferimenti locali alle classi per comodità.

   1. Espandi il file `MediaSDK-js-v2.*.zip` scaricato.
   1. Verifica che il file `MediaSDK.min.js` esiste nella directory `libs`:

   1. Ospita il file `MediaSDK.min.js`.

      Questi file core JavaScript devono essere in hosting su un server Web accessibile a tutte le pagine del sito. È necessario definire il percorso di questi file nella fase successiva.

   1. Fai riferimento a `MediaSDK.min.js` su tutte le pagine del sito.

      Includi `MediaSDK` per JavaScript aggiungendo la seguente riga di codice nel tag `<head>` o `<body>` su ogni pagina. Ad esempio:

      ```
      <script type="text/javascript"
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. Per verificare rapidamente che la libreria sia stata importata correttamente, crea un’istanza della classe `ADB.va.MediaHeartbeatConfig`.

      >[!NOTE]
      >
      >Dalla versione 2.1.0, l’SDK JavaScript è conforme alle specifiche dei moduli AMD e CommonJS e `VideoHeartbeat.min.js` può essere utilizzato anche con caricatori di moduli compatibili.

1. Per un facile accesso alle API, crea riferimenti locali alle classi `MediaHeartbeat`.

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   ```

1. Crea un’istanza `MediaHeartbeatConfig`.

   Questa sezione ti aiuta a capire parametri di configurazione `MediaHeartbeat` e come impostare i valori di configurazione corretti sull’istanza `MediaHeartbeat`, per un tracciamento accurato.

   Esempio di inizializzazione di `MediaHeartbeatConfig`:

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

1. Implementa il protocollo `MediaHeartbeatDelegate`.

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

1. Crea l’istanza `MediaHeartbeat`.

   Utilizza `MediaHeartbeatConfig` e `MediaHeartbeatDelegate` per creare l’istanza `MediaHeartbeat`.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Assicurati che l’istanza `MediaHeartbeat` sia accessibile e non venga deassegnata fino alla fine della sessione multimediale. Questa istanza verrà utilizzata per tutti gli eventi di tracciamento seguenti.

   >[!TIP]
   >
   >`MediaHeartbeat` richiede un’istanza di `AppMeasurement` per inviare chiamate ad Adobe Analytics. Ecco un esempio di un’istanza `AppMeasurement`:

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   appMeasurement.account = <rsid>;
   appMeasurement.pageName = <page_name>;
   appMeasurement.charSet = "UTF­8";
   ```

## Migrare da JavaScript 1.x a 2.x

Nella versione 2.x, tutti i metodi pubblici sono consolidati nella classe `ADB.va.MediaHeartbeat` per agevolare gli sviluppatori. Inoltre, tutte le configurazioni sono ora consolidate nella classe `ADB.va.MediaHeartbeatConfig`.

Per informazioni sulla migrazione dalla versione 1.x alla versione 2.x, consulta la documentazione dell’implementazione legacy.
