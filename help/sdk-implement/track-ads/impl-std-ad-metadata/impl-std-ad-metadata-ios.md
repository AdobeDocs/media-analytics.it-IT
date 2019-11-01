---
title: Implementazione di metadati di annunci standard su iOS
description: Come utilizzare i metadati di annunci standard nel tracciamento di annunci su iOS.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementazione di metadati di annunci standard su iOS{#implement-standard-ad-metadata-on-ios}

## Costanti annuncio

| Nome costante | Descrizione   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Costante per l'associazione di metadati di annunci standard su `AdInfo ADBMediaObject` |

## Implementazione di metadati annuncio standard

Per i metadati di annunci standard, create un dizionario di coppie di valori chiave standard e metadati utilizzando le chiavi per la vostra piattaforma:

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[Chiavi di metadati iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
