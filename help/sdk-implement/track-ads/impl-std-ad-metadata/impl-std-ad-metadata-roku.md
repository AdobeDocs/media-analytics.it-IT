---
title: Scopri come implementare i metadati standard di annunci su Roku
description: Come utilizzare i metadati standard degli annunci nel tracciamento degli annunci su Roku.
uuid: 20a437d7-18b8-4099-ac81-9f3628384236
exl-id: d2c0a1e0-8d40-4f60-a82d-5860550ac152
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 15%

---

# Implementazione dei metadati standard di annunci su Roku{#implement-standard-ad-metadata-on-roku}

## Implementazione dei metadati standard di annunci

Per i metadati standard di annunci, crea un dizionario di coppie di valori chiave di annunci standard utilizzando le chiavi per la piattaforma:

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```
