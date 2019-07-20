---
seo-title: Ripresa delle sessioni inattive
title: Ripresa delle sessioni inattive
uuid: 3 ff 1205 d -7 bbe -4016-9 bd 7-6 e 34 b 7862 c 4 c
translation-type: tm+mt
source-git-commit: 8c20af925a1043c90b84d7d13021848725e05500

---


# Resuming inactive sessions{#resuming-inactive-sessions}

## Pause lunghe

Media SDK monitora automaticamente quanto tempo la riproduzione del file multimediale si trova in uno dei seguenti stati inattivi:

* In pausa
* Ricerca
* Bloccato
* Buffering

Se una sessione di tracciamento multimediale rimane inattiva per oltre 30 minuti, la sessione verrà chiusa automaticamente. If the user resumes after a previously inactive video tracking session (`trackPlay`), Media Heartbeat automatically creates a new video session using the previously used video information and metadata, and sends a resume heartbeat event. For more information, see [Audio and video parameters.](../../metrics-and-metadata/audio-video-parameters.md)

## Riprende manualmente la sessione chiusa precedentemente

Se l'applicazione non è stata chiusa, Media SDK riprende automaticamente le sessioni. Se l'applicazione memorizza i dati utente e ha la possibilità di riprendere un supporto chiuso in precedenza, è possibile attivare manualmente un evento di ripresa. Quando avviate la sessione di tracciamento video, impostate la proprietà opzionale Video Resumed (Riprendi video).

### Android

```java
// Set MediaHeartbeat.MediaObjectKey.mediaResumed to true 
public void onmediaLoad(Observable observable, Object data) { 

  // Replace <MEDIA_NAME> with the media name. 
  // Replace <MEDIA_ID> with a media unique identifier. 
  // Replace <MEDIA_LENGTH> with the media length.  
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
      <MEDIA_NAME>,  
      <MEDIA_ID>,  
      <MEDIA_LENGTH>,  
      MediaHeartbeat.StreamType.VOD 
  ); 
   
  // Set to true if this is a resume playback scenario 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.mediaResumed, true);
   
  _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
}
```

### iOS

```
- (void)onMainmediaLoaded:(NSNotification *)notification { 
  //Replace <MEDIA_NAME> with the media name. 
  //Replace <MEDIA_ID> with a media unique identifier. 
  //Replace <MEDIA_LENGTH> with the media length.     
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME> 
                       mediaId:<MEDIA_ID> 
                       length:<MEDIA_LENGTH> 
                       streamType:ADBMediaHeartbeatStreamTypeVOD]; 

  //Set to YES if this user is resuming a previously closed media session 
  [mediaObject setValue:@(YES) forKey:ADBMediaObjectKeymediaResumed];

  [_mediaHeartbeat trackSessionStart:mediaObject data:mediaMetadata]; 
} 
```

### JavaScript

```js
_onmediaLoad = function () { 
  // Replace <MEDIA_NAME> with the media name. 
  // Replace <MEDIA_ID> with a media unique identifier. 
  // Replace <MEDIA_LENGTH> with the media length.  
  var mediaObject =  
    MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,  
                                     MediaHeartbeat.StreamType.VOD);

  // Set to true if this user is resuming a previously closed media session 
  mediaObject.setValue(MediaObjectKey.mediaResumed, true); 
  this._mediaHeartbeat.trackSessionStart(mediaObject, contextData); 
};
```

