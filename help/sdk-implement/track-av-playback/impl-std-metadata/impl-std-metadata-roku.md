---
title: Implementare i metadati standard su Roku
description: Descrive l’impostazione di video e metadati di annunci standard da inviare con le chiamate di tracciamento su Roku.
uuid: ae14d809-343f-452c-832a-f94bd3d83a90
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

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

