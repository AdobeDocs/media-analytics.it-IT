---
description: nulle
seo-description: nulle
seo-title: Implementazione di metadati di annunci standard in JavaScript
title: Implementazione di metadati di annunci standard in JavaScript
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Implementazione di metadati di annunci standard in JavaScript{#implement-standard-ad-metadata-on-javascript}

## Costanti annuncio

| Nome costante | Descrizione   |
|---|---|
| `StandardAdMetadata` | Costante per l'associazione di metadati di annunci standard su oggetto annuncio |

## Implementazione di metadati annuncio standard

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

