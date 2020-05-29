---
title: Implementazione di metadati di annunci standard tramite JavaScript 3.x
description: Come utilizzare i metadati di annunci standard nel tracciamento degli annunci in un browser utilizzando le app JavaScript 3.x.
translation-type: tm+mt
source-git-commit: 83b38ac8f7fc88f982d194e776efccf8d5b983e4
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
adMetadata[MediaHeartbeat.AdMetadataKeys.Advertiser] = "Sample Advertiser";
adMetadata[MediaHeartbeat.AdMetadataKeys.CampaignId] = "Sample Campaign";

tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
```
