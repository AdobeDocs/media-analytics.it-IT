---
title: Implementazione di metadati di annunci standard tramite JavaScript 3.x
description: Come utilizzare i metadati di annunci standard nel tracciamento degli annunci in un browser utilizzando le app JavaScript 3.x.
translation-type: tm+mt
source-git-commit: 30ed54924c75a9c33e6122b2d7ddbb84c06b8c0c
workflow-type: tm+mt
source-wordcount: '54'
ht-degree: 0%

---


# Implementazione di metadati di annunci standard tramite JavaScript 3.x{#implement-standard-ad-metadata-on-javascript}

## Implementazione di metadati di annunci standard

Per i metadati di annunci standard, create un dizionario di coppie di valori chiave standard e metadati utilizzando le chiavi per la vostra piattaforma:

```js
var adObject =
ADB.Media.createAdObject(<AD_NAME>,
                              <AD_ID>,
                              <POSITION>,
                              <LENGTH>);

// Set standard Ad Metadata
var adMetadata = {};
adMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
adMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";

tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
```
