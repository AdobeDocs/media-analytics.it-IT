---
title: '"Migrazione dall’SDK di Media standalone ad Adobe Launch - Web (JS)"'
description: Scopri come migrare da Media SDK a Launch per JS.
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: ceef739641ae07ea05314fb2bc23028de6ee5efb
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 6%

---

# Migrazione dall’SDK di Media autonomo ad Adobe Launch - Web (JS)

## Differenze tra le funzioni

* *Launch*  - Launch offre un’interfaccia utente che descrive come configurare, configurare e distribuire le soluzioni di tracciamento dei contenuti multimediali basate su Web. Launch migliora Dynamic Tag Management (DTM).
* *Media SDK* : l’SDK per contenuti multimediali fornisce librerie di tracciamento multimediali progettate per piattaforme specifiche (ad esempio: Android, iOS, ecc.). Adobe consiglia Media SDK per il tracciamento dell’utilizzo dei contenuti multimediali nelle app mobili.

## Configurazione

### SDK per contenuti multimediali indipendenti

Nell’SDK di Media autonomo, configuri la configurazione di tracciamento nell’app.
e passalo all&#39;SDK quando crei il tracker.

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

Oltre alla configurazione `MediaHeartbeat`, la pagina deve configurare e trasmettere
l&#39;istanza `AppMeasurement` e l&#39;istanza `VisitorAPI` per il tracciamento dei contenuti multimediali in ordine
per funzionare correttamente.

### Estensione Launch

1. In Experience Platform Launch, fai clic sulla scheda [!UICONTROL Extensions] per
proprietà web.
1. Nella scheda [!UICONTROL Catalog] , individua gli Adobi Medium Analytics for Audio e
Estensione video e fai clic su [!UICONTROL Install].
1. Nella pagina delle impostazioni dell&#39;estensione, configura i parametri di tracciamento.
L’estensione Media utilizza i parametri configurati per il tracciamento.

   ![](assets/launch_config_js.png)

[Guida utente di Launch - Installare e configurare l’estensione multimediale](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html#install-and-configure-the-ma-extension)

## Differenze di creazione del tracciamento

### Media SDK

1. Aggiungi la libreria Media Analytics al tuo progetto di sviluppo.
1. Crea un oggetto config (`MediaHeartbeatConfig`).
1. Implementa il protocollo delegato, esponendo le funzioni `getQoSObject()` e `getCurrentPlaybackTime()` .
1. Crea un&#39;istanza Media Heartbeat (`MediaHeartbeat`).

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
[Media SDK - Tracker Creation](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html) -->

### Launch

Launch offre due approcci per la creazione dell’infrastruttura di tracciamento. Entrambi gli approcci utilizzano l’estensione Media Analytics Launch:

1. Utilizza le API di tracciamento dei contenuti multimediali da una pagina web.

   In questo scenario, l’estensione Media Analytics esporta le API di tracciamento dei contenuti multimediali in una variabile configurata nell’oggetto finestra globale:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Utilizza le API di tracciamento dei contenuti multimediali da un’altra estensione Launch.

   In questo scenario, puoi utilizzare le API di tracciamento dei contenuti multimediali esposte dai moduli condivisi `get-instance` e `media-heartbeat` .

   >[!NOTE]
   >
   >I moduli condivisi non sono disponibili per l’utilizzo nelle pagine web. Puoi utilizzare Moduli condivisi solo da un’altra estensione.

   Crea un&#39;istanza `MediaHeartbeat` utilizzando il modulo condiviso `get-instance`.
Passa un oggetto delegato a `get-instance` che espone le funzioni `getQoSObject()` e `getCurrentPlaybackTime()`.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Accedi alle costanti `MediaHeartbeat` tramite il modulo condiviso `media-heartbeat`.

## Documentazione correlata

### Media SDK

* [Configurazione JavaScript 2.x](/help/sdk-implement/setup/setup-javascript/set-up-js-2.md)
* [Configurazione JavaScript 3.x](/help/sdk-implement/setup/setup-javascript/set-up-js-3.md)
* [API JS Media SDK](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Panoramica di Launch](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)
* [Estensione Media Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html)
