---
title: Scopri come implementare metadati standard di annunci in iOS
description: Come utilizzare i metadati standard degli annunci nel tracciamento degli annunci su iOS.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
exl-id: 018ae833-51d9-4ff0-80e7-3dbcaefb997c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 18%

---

# Implementare metadati standard di annunci su iOS{#implement-standard-ad-metadata-on-ios}

## Costanti di annunci

| Nome costante | Descrizione   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Costante per allegare i metadati standard di annunci su `AdInfo ADBMediaObject` |

## Implementazione dei metadati standard di annunci

Per i metadati standard di annunci, crea un dizionario di coppie di valori chiave di annunci standard utilizzando le chiavi per la piattaforma:

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[Chiavi metadati iOS](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
