---
title: Riproduzione VOD con ricerca nel contenuto principale
description: Visualizza un esempio di come tenere traccia del contenuto VOD in cui si è verificata la ricerca utilizzando Media SDK.
uuid: 5c2392f6-9b9c-42f5-833f-77423d1e6222
exl-id: d77aa717-5dcb-4429-8dce-1914434f2b32
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 6%

---

# Riproduzione VOD con ricerca nel contenuto principale{#vod-playback-with-seeking-in-the-main-content}

## Scenario {#scenario}

Questo scenario include la ricerca nel contenuto principale durante la riproduzione.

Questo è lo stesso scenario della riproduzione [VOD senza scenari di annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md), ma una parte del contenuto viene scorrevole e una ricerca viene completata da un punto del contenuto principale a un altro punto.

| Attivatore   | metodo Heartbeat   | Chiamate di rete   | Note   |
| --- | --- | --- | --- |
| Clic utente [!UICONTROL Play] | `trackSessionStart` | Inizio contenuto Analytics, inizio contenuto Heartbeat | La libreria di misurazione non è a conoscenza dell&#39;esistenza di un annuncio pre-roll, pertanto queste chiamate di rete sono identiche alla riproduzione [VOD senza scenari di annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md). |
| Viene riprodotto il primo fotogramma del contenuto. | `trackPlay` | Riproduzione di contenuti Heartbeat | Quando il contenuto del capitolo viene riprodotto prima del contenuto principale, gli heartbeat iniziano quando il capitolo inizia. |
| Riproduzione di contenuti |  | heartbeat di contenuto | Questa chiamata di rete è esattamente la stessa della riproduzione [VOD senza annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md) scenario. |
| L&#39;utente inizia a cercare l&#39;operazione sul contenuto | `trackSeekStart` |  | Nessun battito cardiaco si spegne fino al completamento della ricerca, ad esempio `trackSeekComplete` |
| Operazione di ricerca completata | `trackSeekComplete` |  | I battiti cardiaci iniziano a uscire dal momento che la ricerca è completa.  Suggerimento:  Il valore della testina di riproduzione deve rappresentare il nuovo playhead corretto dopo la ricerca. |
| Contenuto completato | `trackComplete` | Contenuto Heartbeat completato | Questa chiamata di rete è esattamente la stessa della riproduzione [VOD senza annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md) scenario. |
| Sessione in corso | `trackSessionEnd` |  | `SessionEnd` |

## Codice di esempio {#sample-code}

In questo scenario, l’utente cerca quando il contenuto principale viene riprodotto.

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

Per visualizzare questo scenario, immettere il testo seguente:

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
