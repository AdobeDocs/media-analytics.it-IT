---
title: Implementazione di metadati standard su iOS
description: Descrive l’impostazione di video e metadati di annunci standard da inviare con le chiamate di tracciamento su iOS.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementazione di metadati standard su iOS{#implement-standard-metadata-on-ios}

## Costanti di metadati

| Nome costante | Descrizione   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Costante per l'associazione di metadati standard a `MediaInfo ADBMediaObject` |

## Implementazione

1. Creare un dizionario di coppie di valori chiave di metadati standard utilizzando la variabile `ADBStandardMetadataKeys`
   [Chiavi di metadati IOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Impostate il dizionario di metadati standard sull’ `MediaInfo` `ADBMediaObject` istanza utilizzando la costante Metadati standard per i metadati.

1. Fornire questo `MediaInfo` oggetto durante la chiamata dell' `trackSessionStart` API.

### Esempio di implementazione

Creare un'istanza di un oggetto metdata standard, compilare le variabili desiderate e impostare l'oggetto metadati sull'oggetto Media Heartbeat. Ad esempio:

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

