---
title: Implementazione di metadati di annunci standard tramite JavaScript 2.x
description: Come utilizzare i metadati di annunci standard nel tracciamento degli annunci in un browser utilizzando le app JavaScript 2.x.
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 1%

---


# Implementazione di metadati di annunci standard tramite JavaScript 2.x{#implement-standard-ad-metadata-on-javascript}

## Costanti annuncio

| Nome costante | Descrizione   |
|---|---|
| `StandardAdMetadata` | Costante per l&#39;associazione di metadati di annunci standard su oggetto annuncio |

## Implementazione di metadati di annunci standard

Per i metadati di annunci standard, create un dizionario di coppie di valori chiave standard e metadati utilizzando le chiavi per la vostra piattaforma:

```js
var adObject =  
MediaHeartbeat.createAdObject(<AD_NAME>,  
                              <AD_ID>,  
                              <POSITION>,  
                              <LENGTH>);

// Set standard Ad Metadata
var standardAdMetadata = {};
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
adObject.setValue(MediaObjectKey.StandardAdMetadata, standardAdMetadata);
```
