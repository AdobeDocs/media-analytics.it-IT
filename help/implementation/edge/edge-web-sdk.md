---
title: Inviare dati web ad Edge con Adobe Experience Platform Web SDK
description: Scopri come inviare dati multimediali in streaming di Adobe ad Experience Platform Edge con Adobe Experience Platform Web SDK.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: de40ebd9-46be-4a52-866f-7bb2589fce28
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Inviare dati web ad Edge con Adobe Experience Platform Web SDK

A partire dalla versione 2.20.0, il componente `streamingMedia` di Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/it/docs/experience-platform/web-sdk/home) consente di raccogliere i dati relativi alle sessioni multimediali sul sito Web. I dati raccolti possono includere informazioni su riproduzioni multimediali, pause, completamenti e altri eventi correlati.

Una volta raccolti i dati, puoi inviarli a Adobe Experience Platform e/o Adobe Analytics per generare rapporti. Questa funzione fornisce una soluzione completa per il tracciamento e la comprensione del comportamento di consumo dei contenuti multimediali sul sito web.

Per i clienti che utilizzano Media JS SDK, Web SDK fornisce un percorso di migrazione per passare da Media JS SDK a Web SDK, includendo al contempo il supporto per le funzionalità Media JS esistenti, come la gestione degli eventi multimediali.

## Prerequisiti {#prerequisites}

Per utilizzare il componente `streamingMedia` di Web SDK, è necessario soddisfare i seguenti prerequisiti:

* Prima di poter inviare dati multimediali in streaming ad Edge, completa i passaggi in [Installare la raccolta multimediale in streaming con Experience Platform Edge](/help/implementation/edge/implementation-edge.md).
* Assicurati di avere accesso a Adobe Experience Platform e/o Adobe Analytics.
* È necessario utilizzare Web SDK versione 2.20.0 o successiva. Per informazioni su come installare la versione più recente, consulta la [panoramica sull&#39;installazione di Web SDK](https://experienceleague.adobe.com/it/docs/experience-platform/web-sdk/install/overview).
* Abilitare l&#39;opzione **[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/it/docs/experience-platform/datastreams/configure)** per lo stream di dati in uso.
* Assicurati che lo schema utilizzato dallo stream di dati includa i campi dello schema di Media Collection.
* Configura la funzione Streaming Media nella configurazione del Web SDK, come illustrato in questa pagina, tramite l&#39;[estensione tag](#tag-extension) o tramite la [libreria JavaScript](#library).

Segui i passaggi descritti in questa pagina per migrare l’implementazione di Streaming Media Collection da Media JS a Web SDK.

### Passaggio 1: installare Experience Platform Web SDK

Consulta la [documentazione dedicata](https://experienceleague.adobe.com/it/docs/experience-platform/web-sdk/install/overview) per scoprire come installare Web SDK nelle proprietà Web.

### Passaggio 2: configurare il componente Web SDK `streamingMedia`.

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

È invece necessario configurare il componente `streamingMedia` nel Web SDK come illustrato di seguito.

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

Per informazioni dettagliate su come configurarlo, vedere la [documentazione](https://experienceleague.adobe.com/it/docs/experience-platform/web-sdk/commands/configure/streamingmedia) del componente `streamingMedia` di Web SDK.

### Passaggio 3: ottieni l’istanza di tracciamento dei contenuti multimediali durante la migrazione dal SDK Media JS

Per i clienti che utilizzano Media JS SDK, Web SDK fornisce un percorso di migrazione per passare da Media JS SDK a Web SDK, includendo al contempo il supporto per le funzionalità Media JS esistenti, come la gestione degli eventi multimediali.

[!DNL Web SDK] include un comando per recuperare un tracciatore di Media Analytics. È possibile utilizzare questo comando per creare un&#39;istanza dell&#39;oggetto e quindi, utilizzando le stesse API fornite dalla [libreria Media JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), tenere traccia degli eventi multimediali.

Per informazioni complete sui metodi supportati, consulta la documentazione di [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/it/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker).

Lo snippet seguente mostra come recuperare l’istanza di tracciamento dei contenuti multimediali in Media JS.

```javascript
var tracker = ADB.Media.getInstance();
```

Utilizzare invece il comando `getMediaAnalyticsTracker` in Web SDK per ottenere lo stesso risultato, come illustrato di seguito.

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

Tutti i metodi helper saranno disponibili sull&#39;oggetto `Media`. I metodi di tracciamento sono disponibili nell’istanza di tracciamento, come illustrato di seguito.

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
