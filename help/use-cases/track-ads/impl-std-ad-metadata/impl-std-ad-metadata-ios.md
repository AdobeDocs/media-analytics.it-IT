---
title: Scopri come implementare i metadati standard di annunci su iOS
description: Come utilizzare i metadati standard di annunci nel tracciamento degli annunci su iOS.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
exl-id: 018ae833-51d9-4ff0-80e7-3dbcaefb997c
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 93%

---

# Implementare i metadati standard di annunci su iOS{#implement-standard-ad-metadata-on-ios}

## Costanti di annunci

| Nome costante | Descrizione   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Costante per il collegamento di metadati standard di annunci su `AdInfo ADBMediaObject` |

## Implementare metadati standard di annunci

Per i metadati standard di annunci, crea un dizionario di coppie di valori chiave standard utilizzando le chiavi appropriate per la tua piattaforma:

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[Chiavi metadati iOS](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
