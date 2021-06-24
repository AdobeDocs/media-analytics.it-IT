---
title: Scopri come implementare i metadati standard in Chromecast
description: Scopri come impostare i metadati standard di video e annunci in Chromecast.
uuid: 1560d3e0-29f5-4678-9f01-c672e0ae547b
exl-id: 052ede4b-ea8a-4ca6-bf02-0aab22a8bcda
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 14%

---

# Implementazione dei metadati standard in Chromecast{#implement-standard-metadata-on-chromecast}

Creare un&#39;istanza di un oggetto metdata standard, compilare le variabili desiderate e impostare l&#39;oggetto metadati sull&#39;oggetto Media Heartbeat. Ad esempio:

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

Vedi l&#39;elenco completo dei metadati audio e video qui: [Parametri audio e video.](/help/metrics-and-metadata/audio-video-parameters.md)
