---
title: Inviare dati web a Edge con Adobe Experience Platform Web SDK
description: Scopri come inviare dati Adobe Streaming Media ad Experienci Platform Edge con Adobe Experience Platform Web SDK.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: ad40260d29bd5b739184cb551f084565d05e65a7
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Inviare dati web a Edge con Adobe Experience Platform Web SDK

A partire dalla versione 2.20.0 di, `streamingMedia` componente di Adobe Experience Platform [SDK per web](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) consente di raccogliere i dati relativi alle sessioni multimediali sul sito web. I dati raccolti possono includere informazioni su riproduzioni multimediali, pause, completamenti e altri eventi correlati.

Una volta raccolti i dati, puoi inviarli a Adobe Experience Platform e/o Adobe Analytics per generare rapporti. Questa funzione fornisce una soluzione completa per il tracciamento e la comprensione del comportamento di consumo dei contenuti multimediali sul sito web.

Per i clienti che utilizzano Media JS SDK, Web SDK fornisce un percorso di migrazione per passare da Media JS SDK a Web SDK, includendo al contempo il supporto per le funzionalità Media JS esistenti, come la gestione degli eventi multimediali.

## Prerequisiti {#prerequisites}

Per utilizzare `streamingMedia` componente di Web SDK, è necessario soddisfare i seguenti prerequisiti:

* Prima di poter inviare i dati di Media Analytics a Edge, completa i passaggi descritti in [Installare Media Analytics con Experienci Platform Edge](/help/implementation/edge/implementation-edge.md).
* Assicurati di avere accesso a Adobe Experience Platform e/o Adobe Analytics.
* È necessario utilizzare Web SDK versione 2.20.0 o successiva. Consulta la [Panoramica sull’installazione di Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) per scoprire come installare la versione più recente.
* Abilita **[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)** per lo stream di dati in uso.
* Assicurati che lo schema utilizzato dallo stream di dati includa i campi dello schema di Media Collection.
* Configura la funzione Streaming Media nella configurazione dell’SDK Web, come mostrato in questa pagina, tramite [estensione tag](#tag-extension) o tramite [Libreria JavaScript](#library).

Segui i passaggi descritti in questa pagina per migrare l’implementazione di Analytics para mídia de streaming da Media JS a Web SDK.

### Passaggio 1: installare Experienci Platform Web SDK

Consulta la [documentazione dedicata](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) per scoprire come installare Web SDK nelle proprietà web.

### Passaggio 2: configurare l’SDK web `streamingMedia` componente.

**Esempio**

Lo snippet seguente mostra come configurare la raccolta multimediale in Media JS.

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

È invece necessario configurare `streamingMedia` nell’SDK per web, come illustrato di seguito.

```js
alloy("configure", {
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

Consulta Web SDK `streamingMedia` componente [documentazione](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/streamingmedia) per informazioni complete su come configurarlo.

### Passaggio 3: ottieni l’istanza di tracciamento dei contenuti multimediali durante la migrazione dall’SDK Media JS

Per i clienti che utilizzano Media JS SDK, Web SDK fornisce un percorso di migrazione per passare da Media JS SDK a Web SDK, includendo al contempo il supporto per le funzionalità Media JS esistenti, come la gestione degli eventi multimediali.

[!DNL Web SDK] include un comando per recuperare un tracciatore Media Analytics. È possibile utilizzare questo comando per creare un&#39;istanza dell&#39;oggetto e quindi, utilizzando le stesse API fornite da [Libreria JS per contenuti multimediali](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), tieni traccia degli eventi multimediali.

Consulta la [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker) la documentazione per i dettagli completi sui metodi supportati.

Lo snippet seguente mostra come recuperare l’istanza di tracciamento dei contenuti multimediali in Media JS.

```javascript
var tracker = ADB.Media.getInstance();
```

Invece, utilizza `getMediaAnalyticsTracker` nell’SDK per web per ottenere lo stesso risultato, come illustrato di seguito.

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

Tutti i metodi helper saranno disponibili sul `Media` oggetto. I metodi di tracciamento sono disponibili nell’istanza di tracciamento, come illustrato di seguito.

```js
const mediaInfo = Media.createMediaObject(
  "video name",
  "player video",
  60,
  Media.StreamType.VOD,
  Media.MediaType.Video
);

const contextData = {
  isUserLoggedIn: "false",
  tvStation: "Sample TV station",
  programmer: "Sample programmer",
  assetID: "/uri-reference"
};

// Set standard Video Metadata
contextData[Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[Media.VideoMetadataKeys.Show] = "Sample Show";

trackerInstance.trackSessionStart(mediaInfo, contextData);
```
