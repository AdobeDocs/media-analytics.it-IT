---
title: Configurare Media SDK con JavaScript 2.x
description: Segui questi passaggi per configurare l’applicazione Media SDK su JavaScript 2.x.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
exl-id: 33976096-8b86-4353-906b-e25bf4693471
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '399'
ht-degree: 100%

---

# Configurare JavaScript 2.x{#set-up-javascript}

## Prerequisiti 

* **Ottenere parametri di configurazione validi**
Questi parametri possono essere ottenuti da un rappresentante di Adobe dopo la configurazione dell’account di analisi.
* **Implementa `AppMeasurement` per JavaScript nell’applicazione multimediale**
Per ulteriori informazioni sull’SDK di Adobe Mobile, consulta [Implementazione di Analytics tramite JavaScript.](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=it)

* **Fornisci le seguenti funzionalità nel lettore multimediale:**

   * *API per abbonarsi agli eventi del lettore*: Media SDK richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.
   * *API che fornisce informazioni sul lettore* - Queste informazioni includono dettagli quali il nome del file multimediale e la posizione dell&#39;indicatore di riproduzione.

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
