---
title: '"Migrazione dall’SDK di Media standalone ad Adobe Launch - Web (JS)"'
description: Scopri come migrare da Media SDK a Launch per JS.
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: f0abffb48a6c0babb37f16aff2e3302bf5dd0cb4
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 12%

---

# Migrazione dall’SDK di Media autonomo ad Adobe Launch - Web (JS)

>[!NOTE]
>Adobe Experience Platform Launch è stato riclassificato come una suite di tecnologie di raccolta dati nell’Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=en) come riferimento consolidato delle modifiche terminologiche.

## Differenze tra le funzioni

* *Launch* - Launch offre un’interfaccia utente che descrive come configurare, configurare e distribuire le soluzioni di tracciamento dei contenuti multimediali basate su Web. Launch migliora Dynamic Tag Management (DTM).
* *Media SDK* - Media SDK fornisce librerie di tracciamento dei contenuti multimediali progettate per piattaforme specifiche (ad esempio: Android, iOS, ecc.). Adobe consiglia Media SDK per il tracciamento dell’utilizzo dei contenuti multimediali nelle app mobili.

## Configurazione

### SDK per contenuti multimediali indipendenti

Nell’SDK di Media autonomo, configuri la configurazione di tracciamento nell’app e la trasmetti all’SDK quando crei il tracker.

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

Oltre al `MediaHeartbeat` la pagina deve configurare e trasmettere la `AppMeasurement` istanza e `VisitorAPI` istanza per il tracciamento dei contenuti multimediali per funzionare correttamente.

### Estensione Launch

1. In Experience Platform Launch, fai clic sul pulsante [!UICONTROL Extensions] scheda per la proprietà Web.
1. Sulla [!UICONTROL Catalog] Individua l’estensione Adobe Medium Analytics for Audio and Video e fai clic su [!UICONTROL Install].
1. Nella pagina delle impostazioni dell&#39;estensione, configura i parametri di tracciamento.
L’estensione Media utilizza i parametri configurati per il tracciamento.

   ![](assets/launch_config_js.png)

[Guida utente di Launch - Installare e configurare l’estensione multimediale](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html#install-and-configure-the-ma-extension)

## Differenze di creazione del tracciamento

### Media SDK

1. Aggiungi la libreria Media Analytics al tuo progetto di sviluppo.
1. Crea un oggetto di configurazione (`MediaHeartbeatConfig`).
1. Implementa il protocollo delegato, esponendo il `getQoSObject()` e `getCurrentPlaybackTime()` funzioni.
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

   In questo scenario, puoi utilizzare le API di tracciamento dei contenuti multimediali esposte dalla `get-instance` e `media-heartbeat` Moduli condivisi.

   >[!NOTE]
   >
   >I moduli condivisi non sono disponibili per l’utilizzo nelle pagine web. Puoi utilizzare Moduli condivisi solo da un’altra estensione.

   Crea un `MediaHeartbeat` l&#39;utilizzo dell&#39;istanza `get-instance` Modulo condiviso.
Passa un oggetto delegato a `get-instance` che espone `getQoSObject()` e `getCurrentPlaybackTime()` funzioni.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Accesso `MediaHeartbeat` costanti tramite `media-heartbeat` Modulo condiviso.

## Documentazione correlata

### Media SDK

* [Configurazione JavaScript 2.x](/help/sdk-implement/setup/setup-javascript/set-up-js-2.md)
* [Configurazione JavaScript 3.x](/help/sdk-implement/setup/setup-javascript/set-up-js-3.md)
* [API JS Media SDK](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Panoramica di Launch](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it)
* [Estensione Media Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html)
