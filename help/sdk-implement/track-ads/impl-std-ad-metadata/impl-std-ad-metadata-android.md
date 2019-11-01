---
title: Implementazione di metadati di annunci standard su Android
description: Come utilizzare i metadati di annunci standard nel tracciamento di annunci su Android.
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementazione di metadati di annunci standard su Android{#implement-standard-ad-metadata-on-android}

## Costanti annuncio

| Nome costante | Descrizione   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Costante per allegare metadati di annunci standard su Annuncio `MediaObject`. |

## Implementazione di metadati annuncio standard

Per i metadati di annunci standard, create un dizionario di coppie di valori chiave standard e metadati utilizzando le chiavi per la vostra piattaforma:

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

