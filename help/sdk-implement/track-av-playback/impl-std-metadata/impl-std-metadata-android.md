---
description: nulle
seo-description: nulle
seo-title: Implementare i metadati standard su Android
title: Implementare i metadati standard su Android
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
translation-type: tm+mt
source-git-commit: 46797deb402fed1c4d4781507c279407f8c13f2e

---


# Implementare i metadati standard su Android{#implement-standard-metadata-on-android}

## Costanti metadati standard

| Nome costante | Descrizione   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | Costante per l’associazione di metadati standard a `MediaObject`. |

## Riferimento API per le chiavi di metadati

* Create una serie `HashMap` di coppie standard di valori di metadati.
   * [Tasti di metadati video](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [Chiavi metadati audio](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* Impostate i metadati standard `HashMap` su `MediaInfo` usando la costante Metadati standard per i metadati.
* Fornire questo `MediaInfo` oggetto durante la chiamata dell' `trackSessionStart()` API.

## Implementazioni di esempio

### Video

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardVideoMetadata= new HashMap<String, String>(); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, "Sample Episode"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, "Sample Show"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, "Sample Season"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
```

### Audio

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardAudiooMetadata= new HashMap<String, String>(); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ARTIST, "Sample Artist"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ALBUM, "Sample Album"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.LABEL, "Sample Label"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAudiooMetadata, standardAudiooMetadata);
```
