---
title: "Migrazione da Media SDK standalone ad Adobe Launch - Web (JS)"
description: Scopri come effettuare la migrazione da Media SDK a Launch per JS.
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 73ef5e55c9ab57a5a2ba22aa1e4b646c530cc53f
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 100%

---

# Migrazione da Media SDK ad Adobe Launch - Web (JS)

>[!NOTE]
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=it) come riferimento consolidato delle modifiche terminologiche.

## Differenze nelle funzioni

* *Launch* - Launch offre un’interfaccia utente che ti guida attraverso le operazioni di impostazione, configurazione e implementazione delle soluzioni basate su Web di tracciamento di contenuti multimediali. Launch offre funzionalità migliori rispetto a Dynamic Tag Management (DTM).
* *Media SDK* - Media SDK offre librerie di tracciamento dei contenuti multimediali progettate per piattaforme specifiche (Android, iOS, ecc.). Adobe consiglia di usare Media SDK per il tracciamento dell’utilizzo dei contenuti multimediali nelle app mobili.

## Configurazione

### SDK per contenuti multimediali indipendenti

In Media SDK standalone, puoi configurare le impostazioni di tracciamento nell’app
e trasferirle all’SDK al momento della creazione del tracker.

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

Oltre alla configurazione `MediaHeartbeat`, per funzionare correttamente la pagina deve configurare e trasmettere
l’istanza `AppMeasurement` e l’istanza `VisitorAPI` per il tracciamento dei contenuti multimediali.

### Estensione Launch

1. In Experience Platform Launch, fai clic sulla scheda [!UICONTROL Extensions] per 
la tua proprietà web.
1. Nella scheda [!UICONTROL Catalog], individua l’estensione Adobe Media Analytics for Audio and
Video e fai clic su [!UICONTROL Install].
1. Nella pagina delle impostazioni dell’estensione, configura i parametri di tracciamento.
L’estensione Media utilizza i parametri configurati per il tracciamento.

   ![](assets/launch_config_js.png)

[Guida utente di Launch - Installare e configurare l’estensione per contenuti multimediali](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=it#install-and-configure-the-ma-extension)

## Differenze nella creazione del tracker

### Media SDK

1. Aggiungi la libreria Media Analytics al tuo progetto di sviluppo.
1. Crea un oggetto di configurazione (`MediaHeartbeatConfig`).
1. Implementa il protocollo delegato, esponendo le funzioni `getQoSObject()` e `getCurrentPlaybackTime()`.
1. Crea un’istanza Media Heartbeat (`MediaHeartbeat`).

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

### Launch

Launch offre due tipologie di approccio per la creazione dell’infrastruttura di tracciamento. Entrambi utilizzano l’estensione Media Analytics Launch:

1. Utilizza le API di tracciamento dei contenuti multimediali da una pagina web.

   In questo scenario, l’estensione Media Analytics esporta le API di tracciamento dei contenuti multimediali in una variabile configurata nell’oggetto finestra globale:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Utilizza le API di tracciamento dei contenuti multimediali da un’altra estensione Launch.

   In questo scenario, puoi utilizzare le API di tracciamento dei contenuti multimediali esposte dai Moduli condivisi `get-instance` e `media-heartbeat`.

   >[!NOTE]
   >
   >I Moduli condivisi non sono disponibili per l’utilizzo nelle pagine web. Puoi utilizzare i Moduli condivisi solo da un’altra estensione.

   Crea un&#39;istanza `MediaHeartbeat` tramite il Modulo condiviso `get-instance`.
Trasferisci un oggetto delegato a `get-instance` che espone le funzioni `getQoSObject()` e `getCurrentPlaybackTime()`.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Accedi alle costanti `MediaHeartbeat` tramite il Modulo condiviso `media-heartbeat`.

## Documentazione correlata

### Media SDK

* [Configurare JavaScript 2.x](/help/legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
* [API JS di Media SDK](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Panoramica di Launch](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it)
* [Estensione Media Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=it)
