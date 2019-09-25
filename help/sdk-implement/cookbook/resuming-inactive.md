---
seo-title: Ripresa delle sessioni inattive
title: Ripresa delle sessioni inattive
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Ripresa delle sessioni inattive{#resuming-inactive-sessions}

## Interruzioni lunghe

L’SDK per file multimediali tiene automaticamente traccia della durata della riproduzione in uno dei seguenti stati inattivi:

* In pausa
* Ricerca
* Bloccato
* Buffering

Se una sessione di tracciamento dei contenuti multimediali rimane inattiva per più di 30 minuti, la sessione viene chiusa automaticamente. Se l’utente riprende dopo una sessione di tracciamento video (`trackPlay`) precedentemente inattiva, Media Heartbeat crea automaticamente una nuova sessione video utilizzando le informazioni video e i metadati utilizzati in precedenza e invia un evento heartbeat di ripresa. Per ulteriori informazioni, consultate Parametri [audio e video.](/help/metrics-and-metadata/audio-video-parameters.md)

## Riprendere manualmente la sessione precedentemente chiusa

Media SDK riprenderà automaticamente le sessioni solo se l'applicazione non è stata chiusa. Se l'applicazione memorizza i dati utente e dispone della capacità di riprendere un supporto precedentemente chiuso, è possibile attivare manualmente un evento di ripresa. All’avvio della sessione di tracciamento video, impostate la proprietà video ripresa facoltativa.

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

