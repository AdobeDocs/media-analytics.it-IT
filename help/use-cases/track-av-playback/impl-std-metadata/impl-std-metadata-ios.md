---
title: Scopri come implementare i metadati standard su iOS
description: Scopri come impostare video e metadati standard di annunci da inviare con le chiamate di tracciamento su iOS.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
exl-id: e0981346-3d3c-4a0c-82a4-19942634fd03
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '100'
ht-degree: 100%

---

# Implementare metadati standard su iOS{#implement-standard-metadata-on-ios}

## Costanti di metadati

| Nome costante | Descrizione   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Costante per il collegamento di metadati standard su `MediaInfo ADBMediaObject` |

## Implementazione

1. Crea un dizionario di coppie di valori standard per la chiave dei metadati utilizzando `ADBStandardMetadataKeys`
   [Chiavi metadati iOS](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Imposta il dizionario metadati standard `MediaInfo` sull’istanza `ADBMediaObject` utilizzando la costante Metadati standard per i metadati.

1. Fornisci l’oggetto `MediaInfo` richiamando l’API `trackSessionStart`.

### Implementazione di esempio

Crea un’istanza di un oggetto metadata standard, popola le variabili desiderate e imposta l’oggetto metadati sull’oggetto Media Heartbeat. Ad esempio:

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
