---
description: nulle
seo-description: nulle
seo-title: Implementare i metadati standard su Android
title: Implementare i metadati standard su Android
uuid: c 48 b 4190-b 062-4 c 4 e -9 c 40-8 dde 4598 a 50 e
translation-type: tm+mt
source-git-commit: 46797deb402fed1c4d4781507c279407f8c13f2e

---


# Implement standard metadata on Android{#implement-standard-metadata-on-android}

## Costanti di metadati standard

| Nome costante | Descrizione   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | Constant for attaching standard metadata on `MediaObject`. |

## Riferimento API per i tasti metadati

* Create a `HashMap` of standard metadata key value pairs.
   * [Tasti video sui metadati](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [Chiavi metadati audio](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* Set the standard metadata `HashMap` on `MediaInfo` using the Standard Metadata constant for the metadata.
* Provide this `MediaInfo` object while invoking the `trackSessionStart()` API.

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
