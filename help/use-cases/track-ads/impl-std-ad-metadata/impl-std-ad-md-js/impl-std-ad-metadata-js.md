---
title: Scopri come implementare i metadati standard di annunci utilizzando JavaScript 2.x
description: Come utilizzare i metadati standard di annunci nel tracciamento degli annunci in un browser utilizzando le app JavaScript 2.x.
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
exl-id: b331db87-ab4e-44fa-a97c-9691974cacd4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '70'
ht-degree: 100%

---

# Implementare i metadati standard di annunci utilizzando JavaScript 2.x{#implement-standard-ad-metadata-on-javascript}

## Costanti di annunci

| Nome costante | Descrizione   |
|---|---|
| `StandardAdMetadata` | Costante per il collegamento di metadati standard di annunci sull’oggetto annuncio |

## Implementare metadati standard di annunci

Per i metadati standard di annunci, crea un dizionario di coppie di valori chiave standard utilizzando le chiavi appropriate per la tua piattaforma:

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
