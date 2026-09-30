---
title: Configurare JavaScript per lo streaming di file multimediali
description: Installa e configura Media SDK for JavaScript (3.x) per le implementazioni multimediali in streaming solo per Analytics.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 3%
---
# Configurare JavaScript per lo streaming di file multimediali

Media SDK for JavaScript (3.x) invia i dati multimediali in streaming direttamente ad Adobe Analytics. In questa pagina viene illustrata l&#39;installazione manuale di JavaScript. Per distribuire SDK tramite i tag, vedere [Configurare l&#39;estensione tag di Media Analytics](javascript-tags.md). Per le nuove implementazioni, è consigliabile utilizzare [Web SDK](/help/implementation/edge/web-sdk.md) per inviare dati ad Adobe Analytics tramite uno stream di dati di Edge Network.

* **Prerequisiti**:
  * Completa la [Panoramica sull&#39;implementazione di sola Analytics](overview.md).
  * Implementa [AppMeasurement](https://experienceleague.adobe.com/it/docs/analytics/implementation/js/overview) e il [Servizio ID visitatore](https://experienceleague.adobe.com/it/docs/analytics/implementation/id/appmeasurement).
  * [Scarica Media SDK per JavaScript](/help/getting-started/download-sdks.md).

## Installare e configurare SDK

1. Host `MediaSDK.js` (dalla directory `libs` scaricata) in un server Web accessibile a tutte le pagine e riferimento ad esso in ogni pagina:

   ```html
   <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH/MediaSDK.js"></script>
   ```

1. Configura Media SDK una volta per pagina, passando l&#39;istanza `appMeasurement` configurata come prerequisito:

   ```js
   var mediaConfig = new ADB.MediaConfig();
   mediaConfig.trackingServer = "<media_collection_server>";
   mediaConfig.playerName = "player_name";
   mediaConfig.channel = "sample_channel";
   mediaConfig.appVersion = "app_version";
   mediaConfig.ssl = true;
   
   ADB.Media.configure(mediaConfig, appMeasurement);
   ```

   >[!NOTE]
   >
   >La variabile `mediaConfig.trackingServer` è il **server di raccolta multimediale** (ad esempio, `[namespace].hb-api.omtrdc.net`). Questo server di raccolta è diverso dal server di tracciamento di Analytics configurato nell&#39;istanza di AppMeasurement.

1. Creare un&#39;istanza di tracciamento con `getInstance`. Mantieni l’istanza accessibile per l’intera sessione multimediale:

   ```js
   var tracker = ADB.Media.getInstance();
   ```

## Tracciare gli eventi multimediali

Una volta creato il tracciatore, tieni traccia di ogni evento multimediale utilizzando il relativo metodo di tracciamento. Consulta la scheda **Media SDK JS 3.x** su ogni pagina [event](/help/implementation/events/overview.md) e [variable](/help/implementation/variables/overview.md) per informazioni sulle chiamate esatte.

## Passaggio successivo

Una volta completata l&#39;implementazione, puoi [Configurare la generazione di rapporti per le implementazioni solo Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Riferimento API di Media SDK per JavaScript 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/APIReference.md)
>* [Migrazione da JS SDK 2.x a 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/MigrationGuide.md)
>* [Configurare l&#39;estensione tag di Media Analytics](javascript-tags.md)
>* [Panoramica eventi](/help/implementation/events/overview.md)
