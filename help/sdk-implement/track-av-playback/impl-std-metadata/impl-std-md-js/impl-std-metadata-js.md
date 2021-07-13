---
title: Scopri come implementare i metadati standard utilizzando JavaScript 2.x
description: Scopri come impostare i video standard e i metadati degli annunci da inviare con le chiamate di tracciamento nelle app del browser (JS 2.x).
uuid: 523d29e3-0a62-40d7-ac74-da645024cdcb
exl-id: 889c294b-ac45-4e82-abb3-88ab70abbc3d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '69'
ht-degree: 8%

---

# Implementazione dei metadati standard tramite JavaScript 2.x{#implement-standard-metadata-on-javascript}

## Costante metadati

| Nome costante | Descrizione   |
| --- | --- |
| `StandardMediaMetadata` | Costante per l&#39;associazione di metadati standard su `MediaObject` |

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
