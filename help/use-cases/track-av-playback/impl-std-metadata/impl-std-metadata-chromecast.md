---
title: Scopri come implementare i metadati standard su Chromecast
description: Scopri come impostare i metadati standard di video e annunci su Chromecast.
uuid: 1560d3e0-29f5-4678-9f01-c672e0ae547b
exl-id: 052ede4b-ea8a-4ca6-bf02-0aab22a8bcda
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 100%

---

# Implementare metadati standard in Chromecast{#implement-standard-metadata-on-chromecast}

Crea un’istanza di un oggetto metadata standard, popola le variabili desiderate e imposta l’oggetto metadati sull’oggetto Media Heartbeat. Ad esempio:

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

Consulta l’elenco completo dei metadati video e audio qui: [Parametri audio e video.](/help/implementation/variables/audio-video-parameters.md)
