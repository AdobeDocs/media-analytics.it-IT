---
description: nulle
seo-description: nulle
seo-title: Implementare i metadati degli annunci standard in javascript
title: Implementare i metadati degli annunci standard in javascript
uuid: 4 ea 10 c 5 a-ae 2 b -45 d 0-aad 3-9 f 10028 ee 7 c 3
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Implement standard ad metadata on JavaScript{#implement-standard-ad-metadata-on-javascript}

## Costanti annuncio

| Nome costante | Descrizione   |
|---|---|
| `StandardAdMetadata` | Costante per allegare metadati pubblicitari standard su Oggetto Ad |

## Metadati annunci standard

Per i metadati degli annunci standard, create un dizionario di coppie di valori chiave di metadati standard utilizzando le chiavi per la piattaforma:

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

