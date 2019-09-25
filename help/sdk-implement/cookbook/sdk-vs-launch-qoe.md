---
seo-title: Comprendere le differenze tra Launch e Media SDK
title: Comprendere le differenze tra Launch e Media SDK
uuid: null
translation-type: tm+mt
source-git-commit: 932af09a0692ef35ab46fb6f34b2dec5f2e1e562

---


# Comprendere le differenze tra Launch e Media SDK

## Differenze tra le funzioni

* *Launch* - Launch offre un’interfaccia utente che descrive come impostare, configurare e distribuire soluzioni di monitoraggio dei contenuti multimediali basate su Web. Launch migliora Gestione dinamica dei tag.
* *SDK* per file multimediali - L’SDK per file multimediali fornisce librerie di tracciamento dei contenuti multimediali progettate per piattaforme specifiche (ad esempio: Android, iOS, ecc.) Adobe consiglia Media SDK per tenere traccia dell’utilizzo dei supporti nelle app mobili.

## Differenze di creazione del tracciatore

### Launch

Launch offre due approcci per la creazione dell'infrastruttura di tracciamento. Entrambi gli approcci utilizzano l’estensione di avvio di Media Analytics:

1. Utilizzate le API di tracciamento dei supporti da una pagina Web.

   In questo scenario, Media Analytics Extension esporta le API di tracciamento dei supporti in una variabile configurata nell’oggetto finestra globale:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Utilizzate le API di tracciamento dei supporti da un'altra estensione Launch.

   In questo scenario, utilizzate le API di tracciamento dei supporti esposte dai moduli `get-instance` e `media-heartbeat` condivisi.

   >[!NOTE]
   >
   >I moduli condivisi non sono disponibili per l'uso nelle pagine Web. È possibile utilizzare i moduli condivisi solo da un'altra estensione.

   Create un' `MediaHeartbeat` istanza utilizzando il modulo `get-instance` condiviso.
Passa un oggetto delegato a `get-instance` che espone `getQoSObject()` e `getCurrentPlaybackTime()` funzioni.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Accedere `MediaHeartbeat` alle costanti tramite il modulo `media-heartbeat` condiviso.

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

## Documentazione correlata

### Launch

* [Panoramica di Launch](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [Estensione MA](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### Media SDK

* [Configurare JS](/help/sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

