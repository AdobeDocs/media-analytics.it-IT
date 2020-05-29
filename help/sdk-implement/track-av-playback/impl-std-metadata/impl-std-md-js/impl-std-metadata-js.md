---
title: Implementare i metadati standard utilizzando JavaScript 2.x
description: Descrive l’impostazione di video e metadati di annunci standard da inviare con le chiamate di tracciamento nelle app browser (JS).
uuid: 523d29e3-0a62-40d7-ac74-da645024cdcb
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 6%

---


# Implementare i metadati standard utilizzando JavaScript 2.x{#implement-standard-metadata-on-javascript}

## Costante metadati

| Nome costante | Descrizione   |
| --- | --- |
| `StandardMediaMetadata` | Costante per l&#39;associazione di metadati standard a `MediaObject` |

## Implementazione

Creare un&#39;istanza di un oggetto metdata standard, compilare le variabili desiderate e impostare l&#39;oggetto metadati sull&#39;oggetto Media Heartbeat. Ad esempio:

```js
_onVideoLoad = function () {
    //Create the Media Object   
    var mediaInfo =  
      MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                       <MEDIA_ID,  
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show";
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SEASON] = "Sample Season";
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode";

    //Set standard Audio Metadata
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ARTIST] = "Sample Artist";
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ALBUM] = "Sample Album";
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.LABEL] = "Sample Label";

    mediaInfo.setValue(MediaObjectKey.StandardMediaMetadata, standardMediaMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```
