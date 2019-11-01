---
title: Contenuto principale live con monitoraggio sequenziale
description: Un esempio di come tenere traccia del contenuto live con il tracciamento sequenziale tramite Media SDK.
uuid: b03477b6-9be8-4b67-a5a0-4cef3cf262ab
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Contenuto principale live con monitoraggio sequenziale{#live-main-content-with-sequential-tracking}

## Scenario {#scenario}

In questo scenario, dopo l'unione del flusso live è disponibile una risorsa live senza annunci riprodotti per 40 secondi.

Questo è lo stesso scenario della riproduzione [VOD senza scenari di annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md) , ma una parte del contenuto viene estesa e una ricerca viene completata da un punto del contenuto principale a un altro punto.

| Attivatore | Metodo Heartbeat |  Chiamate di rete |  Note   |
| --- | --- | --- | --- |
| Clic utente [!UICONTROL Play] | trackSessionStart | Inizio contenuto Analytics, Inizio contenuto Heartbeat | La libreria delle misurazioni non è a conoscenza dell'esistenza di un annuncio pre-roll, pertanto queste chiamate di rete sono identiche alla riproduzione [VOD senza scenari di annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md) . |
| Viene riprodotto il primo fotogramma del contenuto. | trackPlay | Heartbeat Content Play | Quando il contenuto dei capitoli viene riprodotto prima del contenuto principale, i heartbeat iniziano quando inizia il capitolo. |
| Riproduzione di contenuto |  | Heartbeat di contenuto | Questa chiamata di rete è esattamente la stessa della riproduzione [VOD senza scenari di annunci](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md) . |
| Passaggio sessione1 (episodio1 terminato) | trackComplete / trackSessionEnd | Heartbeat Content Complete | Completa significa che session1 per il primo episodio è stato raggiunto e guardato completamente. Prima di iniziare la sessione per il prossimo episodio, questa sessione deve essere terminata. |
| Episode2 avviato (avvio sessione2) | trackSessionStart | Inizio contenuto di Analytics Start Heartbeat Content Start | Questo perché l'utente ha visto il primo episodio e ha continuato a guardare in un altro episodio |
| 1° frame del supporto | trackPlay | Heartbeat Content Play | Questo metodo attiva il timer e da questo momento in avanti, heartbeat verrà inviato ogni 10 secondi fintanto che la riproduzione continua. |
| Riproduzioni contenuto |  | Heartbeat di contenuto |  |
| Durata sessione (episodio 2 terminato) | trackComplete / trackSessionEnd | Heartbeat Content Complete | Completa significa che session2 per il secondo episodio è stato raggiunto e guardato completamente. Prima di iniziare la sessione per il prossimo episodio, questa sessione deve essere terminata. |

## Parametri {#parameters}

### Avvio contenuto Heartbeat

| Parametro | Valore | Note |
|---|---|---|
| `s:sc:rsid` | &lt;ID suite di rapporti Adobe&gt; |  |
| `s:sc:tracking_serve` | &lt;URL del server di tracciamento Analytics&gt; |  |
| `s:user:mid` | `s:user:mid` | Deve corrispondere al valore mid nella chiamata di avvio contenuto di Adobe Analytics |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:media_id` | &lt;Nome file multimediale&gt; |  |
| `s:stream:type` | `live` |  |
| `s:meta:*` | *optional* | Metadati personalizzati impostati per il supporto |

## Heartbeat Content Play {#heartbeat-content-play}

Questo dovrebbe assomigliare quasi esattamente alla chiamata Heartbeat Content Start, ma con la differenza chiave nel parametro "s:event:type". Tutti i parametri devono essere ancora presenti.

| Parametro | Valore | Note |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |

## Heartbeat di contenuto {#content-heartbeats}

Durante la riproduzione dei contenuti multimediali, è presente un timer che invia uno o più heartbeat ogni 10 secondi per i contenuti principali e ogni secondo per gli annunci. Questi heartbeat contengono informazioni su riproduzione, annunci pubblicitari, buffering e molti altri elementi. Il contenuto esatto di ogni heartbeat va oltre l'ambito di questo documento, la cosa fondamentale da convalidare è che i heartbeat vengono attivati in modo coerente mentre la riproduzione continua.

Nei heartbeat dei contenuti, cercate alcuni punti specifici:

| Parametro | Valore | Note |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | &lt;posizione dell'indicatore di riproduzione&gt; ad esempio, 50, 60, 70 | Questo deve riflettere la posizione corrente dell'indicatore di riproduzione. |

## Heartbeat Content Complete {#heartbeat-content-complete}

Al termine della riproduzione di un dato episodio (l'indicatore di riproduzione attraversa il limite dell'episodio), viene inviata una chiamata Heartbeat Content Complete. Questo è simile ad altre chiamate Heartbeat, ma contiene un paio di cose specifiche:

| Parametro | Valore | Note |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

## Codice di esempio {#sample-code}

![](assets/ios-live-noads-multiplesessions.png)

### Android

Di seguito è riportato l'ordine di chiamata API previsto:

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., when there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end of session,  
//    i.e., when the media completes and finishes playing 1st episode/session.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() to end session 1 
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Start tracking session 2 /episode 2 of the same live stream.  
// There is no need to reinstantiate a mediaHeartbeat instance for tracking sesison 2. 
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 5. Call trackSessionStart() when the playhead reaches a point that denotes the 
//    start of session 2 
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 6. Call trackPlay() to start tracking session 2 playback  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 7. Call trackComplete() when the playback reaches the end of session 2,  
//    i.e., the media completes and finishes playing.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 8. Call trackSessionEnd() to end session 2 
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Continue similarly tracking further sessions in the live stream if required 
```

### iOS

Di seguito è riportato l'ordine di chiamata API previsto:

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
  
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
  
// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
  
// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 

// 3. Call trackComplete when the playback reaches the end of session,  
//    i.e., when the media completes and finishes playing the first 
//    episode/session. 
[_mediaHeartbeat trackComplete]; 
....... 
....... 

// 4. Call trackSessionEnd to end session 1 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 

// Start tracking session 2 / episode 2 of the same live stream, No need to  
// reinstantiate mediaHeartbeat instance for tracking sesison 2. 

// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
 
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
 
// 5. Call trackSessionStart when the playhead reaches a point that denotes  
//    start of session 2 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
 
// 6. Call trackPlay to start tracking session 2 playback 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 7. Call trackComplete when the playback reaches the end of session 2,  
//    i.e., when the media completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
........ 
........ 
 
// 8. Call trackSessionEnd to end the session 2 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 

// Continue tracking further sessions in live stream similarly if required 
```

### JavaScript

Di seguito è riportato l'ordine di chiamata API previsto:

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
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end of a session,  
//    i.e., whn playback completes and finishes playing the 1st episode/session. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() to end session 1 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Start tracking session 2/episode 2 of the same live stream. There is no need  
// to reinstantiate a mediaHeartbeat instance for tracking sesison 2. 

// Set up mediaObject 
var mediaInfo2 = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

var mediaMetadata2 = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 5. Call trackSessionStart() when the playhead reaches a point that denotes  
//    the start of session 2 
this._mediaHeartbeat.trackSessionStart(mediaInfo2, mediaMetadata2); 

...... 
...... 

// 6. Call trackPlay() to start tracking session 2 playback 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 7. Call trackComplete() when the playback reaches the end of session 2,  
//    i.e., playback completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 8. Call trackSessionEnd() to end session 2 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Continue tracking further sessions in live stream similarly if required 
```

