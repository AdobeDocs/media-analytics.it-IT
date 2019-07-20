---
description: nulle
seo-description: nulle
seo-title: Implementare i metadati degli annunci standard su Android
title: Implementare i metadati degli annunci standard su Android
uuid: 19 b 98 bc 1-c 659-4182-a 4 ff-b 3340 fe 2453 c
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Implement standard ad metadata on Android{#implement-standard-ad-metadata-on-android}

## Costanti annuncio

| Nome costante | Descrizione   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Constant for attaching standard ad metadata on Ad `MediaObject`. |

## Metadati annunci standard

Per i metadati degli annunci standard, create un dizionario di coppie di valori chiave di metadati standard utilizzando le chiavi per la piattaforma:

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

