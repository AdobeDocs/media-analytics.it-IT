---
description: nulle
seo-description: nulle
seo-title: Implementare i metadati standard su Roku
title: Implementare i metadati standard su Roku
uuid: ae 14 d 809-343 f -452 c -832 a-f 94 bd 3 d 83 a 90
translation-type: tm+mt
source-git-commit: c6c7afee72d21c832be77c723750ae0551793613

---


# Implement standard metadata on Roku{#implement-standard-metadata-on-roku}

Crea un'istanza di un oggetto di metdati standard, compila le variabili desiderate e imposta l'oggetto metadati sull'oggetto Media Heartbeat.

**Video:**

```
standardMetadata = {} 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW] = "sample show" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySEASON] = "sample season" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeyEPISODE] = "sample episode" 

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata 
```

**Audio:**

```
standardMetadata = {} 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyARTIST] = "sample artist" 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyALBUM] = "sample album" 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyLABEL] = "sample label"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata 
```

See the comprehensive list of video metadata here: [Audio and video parameters](../../../metrics-and-metadata/audio-video-parameters.md)
