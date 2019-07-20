---
description: nulle
seo-description: nulle
seo-title: Implementare i metadati standard su Chromecast
title: Implementare i metadati standard su Chromecast
uuid: 1560 d 3 e 0-29 f 5-4678-9 f 01-c 672 e 0 ae 547 b
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Implement standard metadata on Chromecast{#implement-standard-metadata-on-chromecast}

Crea un'istanza di un oggetto di metdati standard, compila le variabili desiderate e imposta l'oggetto metadati sull'oggetto Media Heartbeat. Ad esempio:

```js
var standardVideoMetadata = {}; 
standardVideoMetadata[VideoMetadataKeys.SHOW] = "Sample show"; 
standardVideoMetadata[VideoMetadataKeys.SEASON] = "Sample season"; 
 
mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata;
```

```js
var standardAudioMetadata = {}; 
standardAudioMetadata[AudioMetadataKeys.ARTIST] = "Sample artist"; 
standardAudioMetadata[AudioMetadataKeys.ALBUM] = "Sample album"; 
 
mediaObject[ADBMobile.media.MediaObjectKey.StandardAudioMetadata] = standardAudioMetadata;
```

See the comprehensive list of audio and video metadata here: [Audio and video parameters.](../../../metrics-and-metadata/audio-video-parameters.md)