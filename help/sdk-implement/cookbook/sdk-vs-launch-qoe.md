---
seo-title: Comprendere le differenze tra Launch e Media SDK
title: Comprendere le differenze tra Launch e Media SDK
uuid: null
translation-type: tm+mt
source-git-commit: 932af09a0692ef35ab46fb6f34b2dec5f2e1e562

---


# Comprendere le differenze tra Launch e Media SDK

## Differenze tra le funzionalità

* *Launch* - Launch fornisce un'interfaccia utente che illustra come configurare, configurare e distribuire le soluzioni di tracciamento per contenuti multimediali basate sul Web. Launch migliora la gestione dinamica dei tag (DTM).
* *Media SDK* - Media SDK offre librerie di tracciamento multimediale progettate per piattaforme specifiche (ad es.: Android, iOS, ecc.). Adobe consiglia Media SDK di tenere traccia dell'utilizzo dei supporti nelle app mobili.

## Differenze di creazione tracciatore

### Launch

Launch offre due approcci per creare l'infrastruttura di tracciamento. Entrambi gli approcci utilizzano l'estensione Lancio di Media Analytics:

1. Utilizzate le API di tracciamento multimediali da una pagina Web.

   In questo scenario, Media Analytics Extension esporta le API di tracciamento multimediale a una variabile configurata nell'oggetto finestra globale:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Utilizzate le API di tracciamento multimediale da un'altra estensione Lancio.

   In questo scenario, utilizzate le API di tracciamento multimediali esposte dal `get-instance` modulo e `media-heartbeat` da Moduli condivisi.

   >[!NOTE]
   >
   >I moduli condivisi non sono disponibili per l'uso nelle pagine Web. Potete utilizzare solo i moduli condivisi da un'altra estensione.

   Create un `MediaHeartbeat` 'istanza utilizzando il `get-instance` modulo condiviso.
Passate un oggetto delegato a `get-instance` cui esporre `getQoSObject()` e `getCurrentPlaybackTime()` funzioni.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Accedere `MediaHeartbeat` a costanti tramite il `media-heartbeat` modulo condiviso.

### Media SDK

1. Aggiungi la libreria Media Analytics al progetto di sviluppo.
1. Creare un oggetto di configurazione (`MediaHeartbeatConfig`).
1. Implementare il protocollo delegate, esporre le `getQoSObject()``getCurrentPlaybackTime()` funzioni e.
1. Create un'istanza Media Heartbeat (`MediaHeartbeat`).

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

## Documentazione correlata

### Launch

* [Panoramica di Launch](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [Estensione MA](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### Media SDK

* [Configurare JS](/help/sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

