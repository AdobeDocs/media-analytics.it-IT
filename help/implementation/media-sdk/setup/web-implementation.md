---
title: Come impostare un’implementazione web per Analytics for Streaming Media
description: Scopri come implementare Adobe Streaming Media per le app web.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: aed561d0-defc-4be5-87d3-0f331cdfab34
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 92%

---

# Installare Media SDK tramite JavaScript {#install-web-sdks}

Le informazioni in questa pagina descrivono come installare Web SDK autonomo e configurare JavaScript.

In alternativa, è possibile utilizzare l&#39;estensione Analytics Adobe Medium per implementare la raccolta multimediale Adobe Streaming, come descritto in [Implementare Analytics utilizzando l&#39;estensione Media Analytics](/help/implementation/media-sdk/setup/web-implementation-tags.md).

## Prerequisiti {#prerequesites}

* **Ottenere parametri di configurazione validi**

  Questi parametri possono essere ottenuti da un rappresentante di Adobe dopo la configurazione dell’account di analisi.

* **Implementare `AppMeasurement` e `Experience Cloud Identity Service` per JavaScript nell’applicazione multimediale**

  Per ulteriori informazioni, consulta [Implementazione di Analytics con JavaScript](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=it) e [Implementazione del servizio Experience Cloud Identity](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html?lang=it).

* **Includi le seguenti API nel lettore multimediale**

   * *API per abbonarsi agli eventi del lettore*: Media SDK richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.
   * *Un’API che fornisce informazioni sul lettore*: questo include informazioni sui file multimediali, gli annunci e il capitolo attualmente in riproduzione.

## Configurazione JavaScript 3.x  {#set-up-javascript}

1. Aggiungi la libreria [scaricata](/help/getting-started/download-sdks.md) al progetto. Crea riferimenti locali alle classi per comodità.

   1. Espandi il file `MediaSDK-js-v3*.zip` che hai scaricato.
   1. Verifica che il file `MediaSDK.js` esista nella directory `libs`.

   1. Ospita il file `MediaSDK.js`.

      Questi file core JavaScript devono essere in hosting su un server Web accessibile a tutte le pagine del sito. È necessario definire il percorso di questi file nella fase successiva.

   1. Fai riferimento a `MediaSDK.js` su tutte le pagine del sito.

      Includi `MediaSDK` per JavaScript aggiungendo la seguente riga di codice nel tag `<head>` o `<body>` su ogni pagina. Ad esempio:

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. Per verificare rapidamente che la libreria sia stata importata correttamente, controlla che `ADB.Media` sia esportato su un oggetto finestra.

      >[!NOTE]
      >
      >L’SDK per JavaScript è conforme alle specifiche del modulo AMD e CommonJS e `MediaSDK.js` può essere utilizzato anche con caricatori di moduli compatibili.

1. Crea un’istanza di `AppMeasurement` e configura `visitor`.

   La configurazione di Media SDK richiede un’istanza di `AppMeasurement` con `visitor` configurato.

   ```js
    var appMeasurement = new AppMeasurement("<rsid>");
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   ```

1. Configurare Media SDK

   Media SDK deve essere configurato una volta per pagina web e la configurazione si applica a tutte le istanze di tracciamento create.

   >[!IMPORTANT]
   >
   > Media SDK (3.x) utilizza l’API Media Collection per il tracciamento dei contenuti multimediali che è diversa dall’endpoint HB utilizzato negli SDK 2.x. Per ulteriori informazioni, contatta il tuo rappresentante di Adobe.

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

1. Crea l’istanza `MediaTracker`.

   Dopo aver configurato Media SDK, è possibile creare istanze di tracciamento per il contenuto multimediale tramite l’API `getInstance`.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >Assicurati che l’istanza `tracker` sia accessibile e non venga deassegnata fino alla fine della sessione multimediale. Questa istanza verrà utilizzata per monitorare tutti gli eventi seguenti per quella sessione.

## Migrare da JavaScript 2.x a 3.x

Per informazioni dettagliate sulla migrazione da 2.x a 3.x, consulta [Migrazione da 2.x a 3.x.](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)

Per i contenuti legacy, consulta [Implementazioni legacy](/help/legacy/media-sdk/setup/setup-overview.md)
