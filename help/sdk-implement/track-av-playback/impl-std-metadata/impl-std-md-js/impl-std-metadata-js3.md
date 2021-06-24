---
title: Scopri come implementare i metadati standard utilizzando JavaScript 3.x
description: Scopri come impostare video standard e metadati di annunci da inviare con le chiamate di tracciamento nelle app del browser (JS 3.x).
exl-id: 228ba000-10e2-4906-8417-265a03367a9b
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 10%

---

# Implementazione dei metadati standard tramite JavaScript 3.x{#implement-standard-metadata-on-javascript}

## Implementazione

Crea un&#39;istanza di un oggetto dati contestuale, compila le variabili di metadati Standard desiderate. Ad esempio:

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
