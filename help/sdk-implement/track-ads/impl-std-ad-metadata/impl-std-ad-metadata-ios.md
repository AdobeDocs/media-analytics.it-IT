---
title: Scopri come implementare metadati standard di annunci su iOS
description: Come utilizzare i metadati standard di annunci nel tracciamento di annunci su iOS.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
exl-id: 018ae833-51d9-4ff0-80e7-3dbcaefb997c
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 13%

---

# Implementazione dei metadati standard di annunci su iOS{#implement-standard-ad-metadata-on-ios}

## Costanti di annunci

| Nome costante | Descrizione   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Costante per allegare metadati standard di annunci su `AdInfo ADBMediaObject` |

## Implementazione dei metadati standard di annunci

Per i metadati standard di annunci, crea un dizionario di coppie di valori chiave di annunci standard utilizzando le chiavi per la piattaforma:

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[Chiavi dei metadati iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
