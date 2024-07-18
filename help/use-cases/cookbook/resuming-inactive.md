---
title: Ripresa di sessioni inattive
description: Scopri come gestire la ripresa di una sessione inattiva.
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 100%

---

# Ripresa di sessioni inattive {#resuming-inactive-sessions}

## Pause lunghe

Media SDK tiene traccia automaticamente della durata della riproduzione in uno dei seguenti stati inattivi:

* In pausa
* Ricerca
* In stallo
* Buffering

Se una sessione di tracciamento dei contenuti multimediali rimane inattiva per più di 30 minuti, verrà automaticamente chiusa. Se l’utente riprende dopo una sessione di tracciamento video precedentemente inattiva (`trackPlay`), Media Heartbeat crea automaticamente una nuova sessione video utilizzando le informazioni video e i metadati utilizzati in precedenza e invia un evento di ripresa heartbeat. Per ulteriori informazioni, consulta [Parametri audio e video.](/help/implementation/variables/audio-video-parameters.md)


## Riprendere manualmente la sessione precedentemente chiusa

Media SDK riprenderà automaticamente le sessioni solo se l’applicazione non è stata chiusa. Se l’applicazione memorizza i dati utente e dispone della capacità di riprendere un elemento multimediale precedentemente chiuso, è possibile attivare manualmente un evento di ripresa. All’avvio della sessione di tracciamento video, imposta la proprietà facoltativa Video Resumed.

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
