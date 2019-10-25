---
seo-title: Riproduzione VOD senza annunci
title: Riproduzione VOD senza annunci
uuid: ee2a1b79-2c2f-42e1-8e81-b62bbdd0d8cb
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# Riproduzione VOD senza annunci{#vod-playback-with-no-ads}

## Scenario {#scenario}

Questo scenario ha una risorsa VOD, senza annunci, che viene riprodotta una volta dall'inizio alla fine.

| Attivatore | Metodo Heartbeat | Chiamate di rete | Note   |
|---|---|---|---|
| Clic utente **[!UICONTROL Play]** | `trackSessionStart` | Inizio contenuto Analytics, Inizio contenuto Heartbeat | Può trattarsi di un evento di riproduzione automatica o di clic su Riproduci utente. |
| Primo fotogramma del supporto | `trackPlay` | Heartbeat Content Play | Questo metodo attiva il timer e da questo momento in avanti, i heartbeat verranno inviati ogni 10 secondi per la durata della riproduzione. |
| Riproduzione di contenuto |  | Heartbeat di contenuto |  |
| Contenuto completato | `trackComplete` | Heartbeat Content Complete | *Completa* significa che è stata raggiunta la fine del playhead. |

## Parametri {#parameters}

Molti degli stessi valori visualizzati nelle chiamate di avvio di contenuti Heartbeat sono visibili anche nelle `Content Start` chiamate di Adobe Analytics. Esistono molti parametri utilizzati da Adobe per compilare i vari rapporti multimediali, ma solo i parametri più importanti sono elencati nella tabella seguente:

### Avvio contenuto Heartbeat

| Parametro | Valore | Note   |
|---|---|---|
| `s:sc:rsid` | &lt;ID suite di rapporti Adobe&gt; |  |
| `s:sc:tracking_server` | &lt;URL del server di tracciamento Analytics&gt; |  |
| `s:user:mid` | deve essere impostato | Deve corrispondere al valore mid nella `Adobe Analytics Content Start` chiamata. |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:media_id` | &lt;Nome file multimediale&gt; |  |
| `s:meta:*` | optional | Metadati personalizzati impostati per il supporto. |

## Heartbeat Content Play {#heartbeat-content-play}

Questi parametri dovrebbero essere quasi identici alla `Heartbeat Content Start` chiamata, ma la differenza chiave è il `s:event:type` parametro. Tutti gli altri parametri dovrebbero ancora esistere.

| Parametro | Valore | Note   |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |

## heartbeat di contenuto {#content-heartbeats}

Durante la riproduzione dei contenuti multimediali, un timer invia almeno un heartbeat ogni 10 secondi. Questi heartbeat contengono informazioni su riproduzione, annunci pubblicitari, buffering e così via. Il contenuto esatto di ciascun heartbeat supera l'ambito di questo documento, ma il problema fondamentale è che i heartbeat vengono attivati in modo coerente durante la riproduzione continua.

Nei heartbeat di contenuto, cercate i seguenti parametri:

| Parametri | Valore | Note   |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | &lt;posizione dell'indicatore di riproduzione&gt; ad esempio, 50,60,70 | Questo parametro riflette la posizione corrente dell'indicatore di riproduzione. |

## Heartbeat Content Complete {#heartbeat-content-complete}

Al termine della riproduzione, ovvero alla fine dell'indicatore di riproduzione, viene inviata una `Heartbeat Content Complete` chiamata. Questa chiamata ha l'aspetto di altre chiamate Heartbeat, ma contiene alcuni parametri specifici:

| Parametri | Valore | Note   |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

## Codice di esempio {#sample-code}

In questo scenario, il contenuto dura 40 secondi. Viene riprodotto fino alla fine senza interruzioni.

![](assets/main-content-regular-playback.png)

### Android

```java
// Set up  mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay  
//    is used, i.e., there's an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts,  
//    i.e., the first frame of media is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end,  
//    i.e., when the media completes and finishes playing.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() when the playback session is over.  
//    This method must be called even if the user does not watch  
//    the media to completion.  
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

### iOS

```
when the user clicks Play 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeVOD]; 

NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 

// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there's an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 

// 2. Call trackPlay when the playback actually starts, i.e., when the  
//    first frame of main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 

// 3. Call trackComplete when the playback reaches the end, i.e.,  
//    when the media completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
........ 
........ 

// 4. Call trackSessionEnd when the playback session is over. This method  
//    must be called even if the user does not watch the media to completion. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript

```js
// Set up mediaObject 

var mediaInfo = MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME, Configuration.MEDIA_ID,  
Configuration.MEDIA_LENGTH,MediaHeartbeat.StreamType.VOD); 
var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 

}; 

// 1. Call trackSessionStart() when the user clicks play, or when autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the main content starts, i.e.,  
//    the first frame of the media content is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end,  
    i.e., the media completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() when the playback session is over.  
//    This method must be called even if the user does not  
//    watch the media to completion. 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........
```

