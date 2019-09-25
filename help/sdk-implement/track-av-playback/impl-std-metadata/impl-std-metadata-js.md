---
description: nulle
seo-description: nulle
seo-title: Implementare i metadati standard in JavaScript
title: Implementare i metadati standard in JavaScript
uuid: 523d29e3-0a62-40d7-ac74-da645024cdcb
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Implementare i metadati standard in JavaScript{#implement-standard-metadata-on-javascript}

## Costante metadati

| Nome costante | Descrizione   |
| --- | --- |
| `StandardMediaMetadata` | Costante per l'associazione di metadati standard a `MediaObject` |

## Implementazione

Creare un'istanza di un oggetto metdata standard, compilare le variabili desiderate e impostare l'oggetto metadati sull'oggetto Media Heartbeat. Ad esempio:

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

