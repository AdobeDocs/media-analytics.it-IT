---
title: Ripresa di sessioni inattive
description: Scopri come gestire la ripresa di una sessione inattiva.
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 5%

---

# Ripresa delle sessioni inattive{#resuming-inactive-sessions}

## lunghe pause

Media SDK tiene traccia automaticamente della durata della riproduzione in uno dei seguenti stati inattivi:

* In pausa
* Ricerca
* In stallo
* Buffering

Se una sessione di tracciamento dei contenuti multimediali rimane inattiva per più di 30 minuti, la sessione verrà automaticamente chiusa. Se l&#39;utente riprende dopo una sessione di tracciamento video precedentemente inattiva (`trackPlay`), Media Heartbeat crea automaticamente una nuova sessione video utilizzando le informazioni video e i metadati utilizzati in precedenza e invia un evento di ripresa heartbeat. Per ulteriori informazioni, consulta [Parametri audio e video.](/help/metrics-and-metadata/audio-video-parameters.md)

## Riprende manualmente la sessione precedentemente chiusa

Media SDK riprenderà automaticamente le sessioni solo se l&#39;applicazione non è stata chiusa. Se l&#39;applicazione memorizza i dati utente e dispone della capacità di riprendere un supporto precedentemente chiuso, è possibile attivare manualmente un evento di ripresa. All’avvio della sessione di tracciamento video, imposta la proprietà Video Resumed opzionale .

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
