---
description: nulle
seo-description: nulle
seo-title: Implementare i metadati degli annunci standard su Roku
title: Implementare i metadati degli annunci standard su Roku
uuid: 20 a 437 d 7-18 b 8-4099-ac 81-9 f 3628384236
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Implement standard ad metadata on Roku{#implement-standard-ad-metadata-on-roku}

## Metadati annunci standard

Per i metadati degli annunci standard, create un dizionario di coppie di valori chiave di metadati standard utilizzando le chiavi per la piattaforma:

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

