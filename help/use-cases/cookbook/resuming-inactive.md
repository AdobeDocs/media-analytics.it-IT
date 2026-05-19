---
title: Ripresa di sessioni inattive
description: Scopri come gestire la ripresa di una sessione inattiva.
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/KT7NfrYlagrMwAjsrbSNR8YUbj5d-ihU8AfJ6wcbgOA
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 37%

---

# Ripresa di sessioni inattive{#resuming-inactive-sessions}

## Pause lunghe

Media SDK tiene traccia automaticamente della durata della riproduzione in uno dei seguenti stati inattivi:

* In pausa
* Ricerca
* In stallo
* Buffering

Se una sessione di tracciamento dei contenuti multimediali rimane inattiva per più di 30 minuti, verrà automaticamente chiusa. Se l’utente riprende dopo una sessione di tracciamento video precedentemente inattiva (`trackPlay`), Media Heartbeat crea automaticamente una nuova sessione video utilizzando le informazioni video e i metadati utilizzati in precedenza e invia un evento di ripresa heartbeat.

## Consegna tra dispositivi tramite il flag di ripresa

Lo stesso meccanismo di ripresa che gestisce la continuazione della sessione in una singola app si applica anche quando un visualizzatore trasferisce la riproduzione tra dispositivi, ad esempio il cast di un video da un telefono cellulare a un televisore o a un ricevitore Chromecast. Poiché ogni dispositivo esegue la propria istanza di Media SDK, per impostazione predefinita vengono create più sessioni. Utilizza il flag di ripresa per unirli in una continuazione logica in modo che Analytics riporti la visualizzazione combinata come un singolo elemento di coinvolgimento, anziché come avvii di file multimediali separati.

**Come implementare:**

1. Sul dispositivo **sorgente** (ad esempio, il telefono), chiamare `trackSessionEnd` quando il visualizzatore avvia il cast. Non chiamare `trackComplete`: il contenuto non è terminato, si sta spostando su un altro dispositivo.
2. Sul dispositivo di destinazione **** (ad esempio, Chromecast), chiamare `trackSessionStart` con il flag di ripresa impostato su `true` e gli stessi metadati di contenuto (nome, ID, lunghezza) utilizzati nel dispositivo di origine. Passa la posizione della testina di riproduzione nel punto in cui il visualizzatore si è fermato sul dispositivo sorgente.
3. Se in seguito il visualizzatore restituisce la riproduzione al dispositivo di origine, ripetere lo stesso pattern: `trackSessionEnd` sulla destinazione e `trackSessionStart` con il flag di ripresa sull&#39;origine.

L&#39;impostazione del flag di ripresa fa sì che Adobe Analytics incrementi [I contenuti riprendano](/help/reporting/metrics/content-resumes.md) invece di [Avvii file multimediali](/help/reporting/metrics/media-starts.md) per la seconda e le successive parti del passaggio di consegne. Poiché non esiste un meccanismo integrato per condividere l’ID sessione tra le istanze di SDK, il flag di ripresa è una dichiarazione lato client che viene trasmessa in base alla logica dell’applicazione quando si sa che il visualizzatore continua una sessione precedente.

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
