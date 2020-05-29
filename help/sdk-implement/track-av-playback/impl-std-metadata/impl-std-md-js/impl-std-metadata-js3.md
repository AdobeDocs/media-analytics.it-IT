---
title: Implementare i metadati standard utilizzando JavaScript 3.x
description: Descrive l’impostazione di video e metadati di annunci standard da inviare con le chiamate di tracciamento nelle app browser (JS).
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 6%

---


# Implementare i metadati standard utilizzando JavaScript 3.x{#implement-standard-metadata-on-javascript}

## Implementazione

Creare un&#39;istanza di un oggetto dati contestuali, compilare le variabili di metadati Standard desiderate. Ad esempio:

```js
_onVideoLoad = function () {
    //Create the Media Object
    var mediaObject =
      ADB.Media.createMediaObject(<MEDIA_NAME>,
                                       <MEDIA_ID,
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var contextData = {};
    contextData = "Sample Show";
    contextData = "Sample Season";
    contextData = "Sample Episode";

    //Set standard Audio Metadata
    var contextData = {};
    contextData = "Sample Artist";
    contextData = "Sample Album";
    contextData = "Sample Label";

    this.tracker.trackSessionStart(mediaObject, contextData);
};
```
