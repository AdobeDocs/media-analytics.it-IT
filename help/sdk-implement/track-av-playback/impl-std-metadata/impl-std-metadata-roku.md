---
description: nulle
seo-description: nulle
seo-title: Implementare i metadati standard su Roku
title: Implementare i metadati standard su Roku
uuid: ae14d809-343f-452c-832a-f94bd3d83a90
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Implementare i metadati standard su Roku{#implement-standard-metadata-on-roku}

Creare un'istanza di un oggetto metdata standard, compilare le variabili desiderate e impostare l'oggetto metadati sull'oggetto Media Heartbeat.

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

Consultate l'elenco completo dei metadati video, qui: Parametri [audio e video](/help/metrics-and-metadata/audio-video-parameters.md)

