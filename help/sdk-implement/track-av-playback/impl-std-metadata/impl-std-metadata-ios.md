---
description: nulle
seo-description: nulle
seo-title: Implementare i metadati standard su iOS
title: Implementare i metadati standard su iOS
uuid: 75 a 80 f 08-4 a 95-49 d 4-a 27 a -8 ce 531 d 64 d 31
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Implement standard metadata on iOS{#implement-standard-metadata-on-ios}

## Costanti dei metadati

| Nome costante | Descrizione   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Constant for attaching standard metadata on `MediaInfo ADBMediaObject` |

## Implementazione

1. Create a dictionary of standard metadata key value pairs using the `ADBStandardMetadataKeys`
   [Tasti di metadati IOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Set the standard metadata dictionary on `MediaInfo` `ADBMediaObject` instance using the Standard Metadata constant for metadata.

1. Provide this `MediaInfo` object while invoking the `trackSessionStart` API.

### Implementazione di esempio

Crea un'istanza di un oggetto di metdati standard, compila le variabili desiderate e imposta l'oggetto metadati sull'oggetto Media Heartbeat. Ad esempio:

```
// Sample implementation for using standard video metadata keys 
 
NSMutableDictionary *standardVideoMetadata = [[NSMutableDictionary alloc] init]; 
 
[standardVideoMetadata setObject:@"Sample Show" forKey:ADBVideoMetadataKeySHOW]; 
 
[standardVideoMetadata setObject:@"Sample Season" forKey:ADBVideoMetadataKeySEASON]; 
 
[standardVideoMetadata setObject:@"Sample Episode" forKey:ADBVideoMetadataKeyEPISODE]; 
 
[mediaObject setValue:standardVideoMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

```
// Sample implementation for using standard audio metadata keys 
 
NSMutableDictionary *standardAudioMetadata = [[NSMutableDictionary alloc] init];  
 
[standardAudioMetadata setObject:@"Sample Album"   forKey:ADBAudioMetadataKeyALBUM];  
 
[standardAudioMetadata setObject:@"Sample Label"   forKey:ADBAudioMetadataKeyLABEL]; 
 
[mediaObject setValue:standardAudioMetadata   forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

