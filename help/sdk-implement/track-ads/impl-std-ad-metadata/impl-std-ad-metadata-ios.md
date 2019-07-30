---
description: nulle
seo-description: nulle
seo-title: Implementare i metadati degli annunci standard su iOS
title: Implementare i metadati degli annunci standard su iOS
uuid: f 15 fb 727-5 a 5 b -46 c 5-bf 12-93 b 376 c 10 fd 1
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Implement standard ad metadata on iOS{#implement-standard-ad-metadata-on-ios}

## Costanti annuncio

| Nome costante | Descrizione   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Constant for attaching standard ad metadata on `AdInfo ADBMediaObject` |

## Metadati annunci standard

Per i metadati degli annunci standard, create un dizionario di coppie di valori chiave di metadati standard utilizzando le chiavi per la piattaforma:

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[Chiavi di metadati iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
