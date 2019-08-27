---
seo-title: Contenuto principale live con tracciamento sequenziale
title: Contenuto principale live con tracciamento sequenziale
uuid: b 03477 b 6-9 be 8-4 b 67-a 5 a 0-4 cef 3 cf 262 ab
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Contenuto principale live con tracciamento sequenziale{#live-main-content-with-sequential-tracking}

## Scenario {#section_E4B558253AD84ED59256EDB60CED02AE}

In questo scenario, esiste una risorsa live senza annunci pubblicitari per 40 sec dopo aver partecipato al flusso live.

Si tratta dello stesso scenario della [riproduzione VOD senza](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md) uno scenario ads, ma una parte del contenuto scorre e una ricerca viene completata da un punto del contenuto principale a un altro punto.

| Attivatore | Heartbeat, metodo | Chiamate di rete  | Note   |
| --- | --- | --- | --- |
| Clic sugli utenti [!UICONTROL Play] | `trackSessionStart` | Inizio del contenuto di Analytics, Inizio contenuto Heartbeat | La libreria delle misurazioni non riconosce che è presente un annuncio prerelease, quindi queste chiamate di rete sono identiche alla riproduzione [VOD senza](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md) uno scenario ads. |
| Viene riprodotto il primo fotogramma del contenuto. | `trackPlay` | Riproduzione contenuto heartbeat | Quando il contenuto dei capitoli viene riprodotto prima del contenuto principale, i Heartbeat iniziano all'avvio del capitolo. |
| Il contenuto viene riprodotto |  | Heartbeats contenuto | Questa chiamata di rete è esattamente identica alla [riproduzione VOD senza](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md) uno scenario ads. |
| Sessione 1 sopra (Episodio 1 terminato) | `trackComplete` `trackSessionEnd` | Heartbeat Content Complete | Complete significa che la sessione 1 st 1 per l'episodio è stata raggiunta e guardata completamente. Prima di avviare la sessione per l'episodio successivo, questa sessione deve essere terminata. |
| Episodio 2 avviato (inizio sessione 2) | `trackSessionStart` | Analytics Content Start Heartbeat Content Start | Questo perché l'utente ha guardato il primo episodio e continuava a guardare un altro episodio |
| 1 st Frame of Media | `trackPlay` | Riproduzione contenuto heartbeat | Questo metodo attiva il timer e da questo momento in poi, heartbebeat verrà inviato ogni 10 secondi finché la riproduzione continua. |
| Il contenuto viene riprodotto |  | Heartbeats contenuto |  |
| Sessione Over (Episodio 2 terminato) | `trackComplete` `trackSessionEnd` | Heartbeat Content Complete | Completato significa che l'episodio della sessione 2 per il 2 nd è stato raggiunto e controllato completamente. Prima di avviare la sessione per l'episodio successivo, questa sessione deve essere terminata. |

## Parametri {#section_D52B325B99DA42108EF560873907E02C}

### Inizio contenuto heartbeat

| Parametro | Valore | Note |
|---|---|---|
| `s:sc:rsid` | &lt; ID suite di rapporti &gt; |  |
| `s:sc:tracking_serve` | &lt; URL del server di tracciamento Analytics &gt; |  |
| `s:user:mid` | `s:user:mid` | Deve corrispondere al valore mid in Adobe Analytics Content Start Call |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:media_id` | &lt; Nome file multimediali &gt; |  |
| `s:stream:type` | `live` |  |
| `s:meta:*` | *facoltativo* | Set di metadati personalizzati sul supporto |

## Riproduzione contenuto heartbeat {#section_B6AD9225747943F881DCA8E6A1D5710E}

Dovrebbe essere simile alla chiamata di Avvio contenuto Heartbeat, ma con la differenza chiave in «s: evento: type ". Tutti i parametri devono essere inseriti qui.

| Parametro | Valore | Note |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |

## Heartbeats contenuto {#section_7B387303851A43E5993F937AE2B146FE}

Durante la riproduzione di contenuti multimediali, esiste un timer che invierà uno o più heartbebeat ogni 10 secondi per il contenuto principale e ogni secondo per annunci. Tali heartbeat contengono informazioni su riproduzione, annunci pubblicitari, buffering e molti altri elementi. Il contenuto esatto di ogni heartbeat va oltre l'ambito di questo documento, il punto critico da convalidare è che i heartbeat vengono attivati in modo coerente mentre la riproduzione continua.

Nei heartbeat del contenuto, cerca alcuni elementi specifici:

| Parametro | Valore | Note |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | &lt; posizione della linea di scansione &gt;, ad esempio 50, 60, 70 | Deve riflettere la posizione corrente dell'indicatore di riproduzione. |

## Heartbeat Content Complete {#section_2CA970213AF2457195901A93FC9D4D0D}

Quando la riproduzione per un determinato episodio è completata (l'indicatore di riproduzione attraversa il limite di un episodio), viene inviata una chiamata Heartbeat Content Complete. Questo aspetto si presenta come altre chiamate Heartbeat, ma contiene un paio di elementi specifici:

| Parametro | Valore | Note |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

## Codice di esempio {#section_mpx_q2j_x2b}

![](assets/ios-live-noads-multiplesessions.png)

### Android

Ecco il previsto ordine delle chiamate API:

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

Ecco il previsto ordine delle chiamate API:

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

Ecco il previsto ordine delle chiamate API:

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

