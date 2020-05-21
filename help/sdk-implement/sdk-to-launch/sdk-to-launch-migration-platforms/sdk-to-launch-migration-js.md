---
title: Migrazione dall’SDK per file multimediali standalone ad Adobe Launch - Web (JS)
description: Istruzioni ed esempi di codice per facilitare la migrazione da Media SDK a Launch.
translation-type: tm+mt
source-git-commit: 0f9a985d04969eeca837a2655c666259ce30aee4
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 6%

---


# Migrazione dall’SDK per file multimediali standalone ad Adobe Launch - Web (JS)

## Differenze tra le funzioni

* *Launch* - Launch offre un’interfaccia utente che descrive come impostare, configurare e distribuire soluzioni di monitoraggio dei contenuti multimediali basate su Web. Launch migliora Gestione dinamica dei tag.
* *SDK* per file multimediali - L’SDK per file multimediali fornisce librerie di tracciamento dei contenuti multimediali progettate per piattaforme specifiche (ad esempio: Android, iOS, ecc.) Adobe consiglia Media SDK per tenere traccia dell’utilizzo dei supporti nelle app mobili.

## Configurazione

### SDK per file multimediali indipendenti

Nell’SDK per file multimediali standalone, configuri la configurazione di tracciamento nell’app e passala all’SDK quando crei il tracciatore.

```javascript
//Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = "namespace.hb.omtrdc.net";
mediaConfig.playerName = "html5-player";
mediaConfig.channel = "sample-channel";
mediaConfig.ovp = "video-provider";
mediaConfig.appVersion = "v2.0.0"
mediaConfig.ssl = true;
mediaConfig.debugLogging = true;
```

Oltre alla `MediaHeartbeat` configurazione, la pagina deve configurare e passare l’ `AppMeasurement` istanza e l’ `VisitorAPI` istanza per il tracciamento dei supporti al fine di funzionare correttamente.

### Avvia estensione

1. In Experience Platform Launch, fai clic sulla [!UICONTROL Extensions] scheda della proprietà Web.
1. Nella [!UICONTROL Catalog] scheda, individua l’estensione Adobe Media Analytics for Audio and Video e fai clic su [!UICONTROL Install].
1. Nella pagina delle impostazioni di estensione, configurate i parametri di tracciamento.
L’estensione Media utilizzerà i parametri configurati per il tracciamento.

   ![](assets/launch_config_js.png)

[Guida utente di Launch - Installare e configurare l&#39;estensione del supporto](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#install-and-configure-the-ma-extension)

## Differenze di creazione del tracciatore

### Media SDK

1. Aggiungi la libreria Media Analytics al tuo progetto di sviluppo.
1. Creare un oggetto config (`MediaHeartbeatConfig`).
1. Implementa il protocollo delegato, esponendo le funzioni `getQoSObject()` e `getCurrentPlaybackTime()` .
1. Create un’istanza di heartbeat multimediale (`MediaHeartbeat`).

```
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
...
// Configuration settings
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
...
// Implement Media Delegate (Quality of Service and Playhead)
var mediaDelegate = new MediaHeartbeatDelegate();
...
mediaDelegate.getQoSObject = function() {
    return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
    ...
}
...
// Create your tracker
this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

<!--  Dead Link - from 2019 - can't locate where this should go
[Media SDK - Tracker Creation](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html) -->

### Launch

Launch offre due approcci per la creazione dell&#39;infrastruttura di tracciamento. Entrambi gli approcci utilizzano l’estensione di avvio di Media Analytics:

1. Utilizzate le API di tracciamento dei supporti da una pagina Web.

   In questo scenario, Media Analytics Extension esporta le API di tracciamento dei supporti in una variabile configurata nell’oggetto finestra globale:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Utilizzate le API di tracciamento dei supporti da un&#39;altra estensione Launch.

   In questo scenario, utilizzate le API di tracciamento dei supporti esposte dai moduli `get-instance` e `media-heartbeat` condivisi.

   >[!NOTE]
   >
   >I moduli condivisi non sono disponibili per l&#39;uso nelle pagine Web. È possibile utilizzare i moduli condivisi solo da un&#39;altra estensione.

   Create un&#39; `MediaHeartbeat` istanza utilizzando il modulo `get-instance` condiviso.
Passa un oggetto delegato a `get-instance` che espone `getQoSObject()` e `getCurrentPlaybackTime()` funzioni.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Accedere `MediaHeartbeat` alle costanti tramite il modulo `media-heartbeat` condiviso.

## Documentazione correlata

### Media SDK

* [Configurare JS](/help/sdk-implement/setup/set-up-js.md)
* [API JS Media SDK](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Panoramica di Launch](https://docs.adobe.com/content/help/it-IT/launch/using/overview.html)
* [Estensione Media Analytics](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
