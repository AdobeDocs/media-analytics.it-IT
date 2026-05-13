---
title: Come impostare un’implementazione web per Analytics for Streaming Media
description: Scopri come implementare Adobe Streaming Media per le app web.
feature: Streaming Media
role: User, Admin, Developer
exl-id: aed561d0-defc-4be5-87d3-0f331cdfab34
TQID: https://experienceleague.adobe.com/UBY26SeGZbGWHjwOm6-YZNET8fe5Gvvco7aIZ9Z7rZg
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 472
ht-degree: 93%

---

# Installare Media SDK tramite JavaScript {#install-web-sdks}

Le informazioni in questa pagina descrivono come installare Web SDK autonomo e configurare JavaScript.

In alternativa, è possibile utilizzare l&#39;estensione Adobe Media Analytics per implementare i servizi di streaming multimediale, come descritto in [Installare i servizi di streaming multimediale tramite l&#39;estensione Media Analytics](/help/implementation/media-sdk/setup/web-implementation-tags.md).

## Prerequisiti {#prerequesites}

* **Ottenere parametri di configurazione validi**

  Questi parametri possono essere ottenuti da un rappresentante di Adobe dopo la configurazione dell’account di analisi.

* **Implementare `AppMeasurement` e `Experience Cloud Identity Service` per JavaScript nell’applicazione multimediale**

  Per ulteriori informazioni, consulta [Implementazione di Analytics con JavaScript](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=it) e [Implementazione del servizio Experience Cloud Identity](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html?lang=it).

* **Includi le seguenti API nel lettore multimediale**

   * *API per abbonarsi agli eventi del lettore*: Media SDK richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.
   * *Un’API che fornisce informazioni sul lettore*: questo include informazioni sui file multimediali, gli annunci e il capitolo attualmente in riproduzione.

## Configurazione JavaScript 3.x {#set-up-javascript}

1. Aggiungi la libreria [scaricata](/help/getting-started/download-sdks.md) al progetto. Crea riferimenti locali alle classi per comodità.

   1. Espandi il file `MediaSDK-js-v3*.zip` scaricato.
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
