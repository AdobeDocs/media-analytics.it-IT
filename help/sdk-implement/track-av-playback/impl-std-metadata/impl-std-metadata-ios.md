---
title: Scopri come implementare metadati standard su iOS
description: Scopri come impostare i video standard e i metadati degli annunci da inviare con le chiamate di tracciamento su iOS.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
exl-id: e0981346-3d3c-4a0c-82a4-19942634fd03
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 10%

---

# Implementazione dei metadati standard su iOS{#implement-standard-metadata-on-ios}

## Costanti metadati

| Nome costante | Descrizione   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Costante per l&#39;associazione di metadati standard su `MediaInfo ADBMediaObject` |

## Implementazione

1. Crea un dizionario di coppie di valori chiave di metadati standard utilizzando `ADBStandardMetadataKeys`
   [Tasti di metadati IOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Imposta il dizionario metadati standard sull&#39;istanza `MediaInfo` `ADBMediaObject` utilizzando la costante metadati standard per i metadati.

1. Fornisci questo oggetto `MediaInfo` durante la chiamata dell&#39;API `trackSessionStart`.

### Implementazione di esempio

Creare un&#39;istanza di un oggetto metdata standard, compilare le variabili desiderate e impostare l&#39;oggetto metadati sull&#39;oggetto Media Heartbeat. Ad esempio:

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
