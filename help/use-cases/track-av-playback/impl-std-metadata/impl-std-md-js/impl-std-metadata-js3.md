---
title: Scopri come implementare i metadati standard utilizzando JavaScript 3.x
description: Scopri come impostare video standard e metadati di annunci da inviare con le chiamate di tracciamento nelle app del browser (JS 3.x).
exl-id: 228ba000-10e2-4906-8417-265a03367a9b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '48'
ht-degree: 6%

---

# Implementazione dei metadati standard tramite JavaScript 3.x{#implement-standard-metadata-on-javascript}

## Implementazione

Crea un&#39;istanza di un oggetto dati contestuale, compila le variabili di metadati Standard desiderate. Esempio:

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
