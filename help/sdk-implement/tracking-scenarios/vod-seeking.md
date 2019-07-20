---
seo-title: Riproduzione VOD con ricerca nel contenuto principale
title: Riproduzione VOD con ricerca nel contenuto principale
uuid: 5 c 2392 f 6-9 b 9 c -42 f 5-833 f -77423 d 1 e 6222
translation-type: tm+mt
source-git-commit: b2d2f7078d655c6e50b3f2925002f93d5a0af533

---


# VOD playback with seeking in the main content{#vod-playback-with-seeking-in-the-main-content}

## Scenario {#section_E4B558253AD84ED59256EDB60CED02AE}

Questo scenario include la ricerca nel contenuto principale durante la riproduzione.

This is the same scenario as the [VOD playback with no ads](../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md) scenario, but a part of the content is scrubbed through and a seek is completed from one point in main content to another point.

| Attivatore   | Heartbeat, metodo  | Chiamate di rete  | Note   |
| --- | --- | --- | --- |
| User clicks [!UICONTROL Play] | `trackSessionStart` | Inizio del contenuto di Analytics, Inizio contenuto Heartbeat | The measurement library is unaware that there is a pre-roll ad, so these network calls are identical to the [VOD playback with no ads](../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md) scenario. |
| Viene riprodotto il primo fotogramma del contenuto. | `trackPlay` | Riproduzione contenuto heartbeat | Quando il contenuto dei capitoli viene riprodotto prima del contenuto principale, i Heartbeat iniziano all'avvio del capitolo. |
| Il contenuto viene riprodotto |  | Heartbeats contenuto | This network call is exactly the same as the [VOD playback with no ads](../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md) scenario. |
| L'utente inizia l'operazione di ricerca sul contenuto | `trackSeekStart` |  | No heartbeats go out till seek is complete, for example, `trackSeekComplete` |
| Operazione di ricerca completata | `trackSeekComplete` |  | Heartbeats inizia a uscire dalla ricerca. Suggerimento: Il valore della linea di scansione deve rappresentare la nuova linea di scansione corretta dopo la ricerca. |
| Il contenuto è completo | `trackComplete` | Heartbeat Content Complete | This network call is exactly the same as the [VOD playback with no ads](../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md) scenario. |
| Sessione over | `trackSessionEnd` |  | `SessionEnd` |

## Codice di esempio {#section_q2d_wcj_x2b}

In questo scenario, l'utente sta cercando quando viene riprodotto il contenuto principale.

![](assets/seek-main-to-main.png)

### Android

Per visualizzare questo scenario in Android, impostate il seguente codice:

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

### App

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

Per visualizzare questo scenario, immettete il testo seguente:

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

