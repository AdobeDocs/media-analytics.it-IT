---
title: 'Riproduzione VOD con ricerca nel contenuto principale '
description: Visualizza un esempio di come tracciare contenuti VOD in cui si è verificata la ricerca utilizzando Media SDK.
uuid: 5c2392f6-9b9c-42f5-833f-77423d1e6222
exl-id: d77aa717-5dcb-4429-8dce-1914434f2b32
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 100%

---

# Riproduzione VOD con ricerca nel contenuto principale {#vod-playback-with-seeking-in-the-main-content}

## Scenario {#scenario}

Questo scenario include la ricerca nel contenuto principale durante la riproduzione.

Questo è lo stesso scenario della [riproduzione VOD senza annunci](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md), ma una parte del contenuto viene eliminata e una ricerca viene completata da un punto del contenuto principale a un altro punto.

| Trigger   | Metodo Heartbeat   | Chiamate di rete   | Note   |
| --- | --- | --- | --- |
| Clic utente [!UICONTROL Play] | `trackSessionStart` | Inizio contenuto Analytics, inizio contenuto Heartbeat | La libreria di misurazione non è a conoscenza dell’esistenza di un annuncio pre-roll, pertanto queste chiamate di rete sono identiche allo scenario [riproduzione VOD senza annunci](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md). |
| Viene riprodotto il primo fotogramma del contenuto. | `trackPlay` | Riproduzione di contenuti Heartbeat | Quando il contenuto del capitolo viene riprodotto prima del contenuto principale, gli heartbeat partono all’inizio del capitolo. |
| Riproduzione dei contenuti | | Heartbeat dei contenuti | Questa chiamata di rete è esattamente la stessa dello scenario [riproduzione VOD senza annunci](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md). |
| L’utente inizia l’operazione di ricerca nel contenuto | `trackSeekStart` | | Non viene inviato alcun heartbeat finché la ricerca non è stata completa, per esempio `trackSeekComplete` |
| Operazione di ricerca completata | `trackSeekComplete` | | Gli heartbeat iniziano a essere inviati dal momento in cui la ricerca è stata completata. Suggerimento: il valore della testina di riproduzione deve rappresentare il nuovo valore corretto dopo la ricerca. |
| Contenuto completato | `trackComplete` | Contenuto Heartbeat completato | Questa chiamata di rete è identica a quella dello scenario [Riproduzione VOD senza annunci](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md). |
| Sessione terminata | `trackSessionEnd` | | `SessionEnd` |

## Codice di esempio {#sample-code}

In questo scenario, l’utente effettua la ricerca mentre viene riprodotto il contenuto principale.

![](assets/seek-main-to-main.png)

### Android

Per visualizzare questo scenario in Android, imposta il seguente codice:

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
mediaMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., whn the first frame  
//    of the main content is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Track the MediaHeartbeat.Event.SeekStart event when the user begins to seek.  
_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 

....... 
....... 

// 4. Track the MediaHeartbeat.Event.SeekComplete event when the user completes seeking 
_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 

....... 
....... 

// 5. Call trackComplete() when the playback reaches the end, i.e., when the media 
//    completes and finishes playing. 
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 6. Call trackSessionEnd() when the playback session is over. This method must be  
//    called even if the user does not watch the media to completion.  
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

### iOS

Per visualizzare questo scenario in iOS, imposta il seguente codice:

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME o 
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeVOD]; 
 
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 

// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
....... 
....... 

// 2. Call trackPlay when the playback actually starts, i.e., when the 
//    first frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay];  
....... 
....... 

// 3. Track the trackEvent:ADBMediaHeartbeatEventSeekStart event when the user  
//    begins to seek out of the chapter with the intent to skip it. 
[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart  
               mediaObject:nil  
               data:nil]; 
....... 
....... 

// 4. Track the trackEvent:ADBMediaHeartbeatEventSeekComplete event when the  
//    user seeks out of the chapter with the intent to skip it. 
[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete  
               mediaObject:nil  
               data:nil]; 
....... 
....... 

// 5. Call trackComplete when the playback reaches the end, i.e., completes  
//    and finishes playing. 
[_mediaHeartbeat trackComplete]; 
....... 
....... 

// 6. Call trackSessionEnd when the playback session is over. This method must  
//    be called even if the user does not watch the media to completion. 
[_mediaHeartbeat trackSessionEnd]; 
....... 
....... 
```

### JavaScript

Per visualizzare questo scenario, immetti il testo seguente:

```js
// Set up mediaObject 
var mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 

); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 

}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of the ad media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Track the MediaHeartbeat.Event.SeekStart event when the user  
//    begins to seek. 
this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 

....... 
....... 

// 4. Track the MediaHeartbeat.Event.SeekComplete event when the user  
//    completes seeking. 
this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 

....... 
....... 

// 5. Call trackComplete() when the playback reaches the end, i.e., when 
//    playback completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 6. Call trackSessionEnd() when the playback session is over. This method must be called  
//    even if the user does not watch the media to completion. 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```
