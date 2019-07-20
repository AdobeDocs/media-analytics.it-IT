---
seo-title: Riproduzione VOD senza annunci
title: Riproduzione VOD senza annunci
uuid: ee 2 a 1 b 79-2 c 2 f -42 e 1-8 e 81-b 62 bbdd 0 d 8 cb
translation-type: tm+mt
source-git-commit: b2d2f7078d655c6e50b3f2925002f93d5a0af533

---


# VOD playback with no ads{#vod-playback-with-no-ads}

## Scenario {#section_E4B558253AD84ED59256EDB60CED02AE}

Questo scenario ha una risorsa VOD, senza annunci, che viene riprodotta una volta dall'inizio alla fine.

| Attivatore | Heartbeat, metodo | Chiamate di rete | Note   |
|---|---|---|---|
| User clicks **[!UICONTROL Play]** | `trackSessionStart` | Inizio del contenuto di Analytics, Inizio contenuto Heartbeat | Può trattarsi di un utente che fa clic su Riproduci o su un evento di riproduzione automatica. |
| Primo fotogramma del supporto | `trackPlay` | Riproduzione contenuto heartbeat | Questo metodo attiva il timer e, da questo momento in poi, heartbeats viene inviato ogni 10 secondi per tutta la durata della riproduzione. |
| Il contenuto viene riprodotto |  | Heartbeats contenuto |  |
| Il contenuto è completo | `trackComplete` | Heartbeat Content Complete | *Completato* significa che è stata raggiunta la fine dell'indicatore di riproduzione. |

## Parametri {#section_45D7B10031524411B91E2C569F7818B0}

Many of the same values that you see on Heartbeat Content Start Calls are also seen on Adobe Analytics `Content Start` Calls. Esistono molti parametri che Adobe utilizza per comporre i vari rapporti multimediali, ma solo i parametri più importanti sono elencati nella tabella seguente:

### Inizio contenuto heartbeat

| Parametro | Valore | Note   |
|---|---|---|
| `s:sc:rsid` | &lt; ID suite di rapporti &gt; |  |
| `s:sc:tracking_server` | &lt; URL del server di tracciamento Analytics &gt; |  |
| `s:user:mid` | deve essere impostato | Should match the mid value on the `Adobe Analytics Content Start` call. |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:media_id` | &lt; Nome file multimediali &gt; |  |
| `s:meta:*` | facoltativo | Metadati personalizzati impostati sul supporto. |

## Heartbeat Content Play {#section_2ABBD51D3A6D45ABA92CC516E414417A}

These parameters should look nearly identical to the `Heartbeat Content Start` call, but the key difference is the `s:event:type` parameter. Tutti gli altri parametri devono ancora esistere.

| Parametro | Valore | Note   |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |

## Content heartbeats {#section_3B5945336E464160A94518231CEE8F53}

Durante la riproduzione di contenuti multimediali, un timer invia almeno un heartbeat ogni 10 secondi. Questi heartbeat contengono informazioni sulla riproduzione, gli annunci pubblicitari, il buffering e così via. Il contenuto esatto di ogni heartbeat va oltre l'ambito di questo documento, ma il problema critico è che i heartbeat vengono attivati in modo coerente mentre la riproduzione continua.

Nei heartbeat del contenuto, cerca i seguenti parametri:

| Parametri | Valore | Note   |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | &lt; posizione della linea di scansione &gt;, ad esempio 50,60,70 | Questo parametro riflette la posizione corrente dell'indicatore di riproduzione. |

## Heartbeat Content Complete {#section_33BCC4C3181940C39446A57C25D82179}

When playback has completed, which means that the end of the playhead is reached, a `Heartbeat Content Complete` call is sent. Questa chiamata si presenta come altre chiamate Heartbeat, ma contiene alcuni parametri specifici:

| Parametri | Valore | Note   |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

## Codice di esempio {#section_glq_vw3_x2b}

In questo scenario, il contenuto è di 40 secondi. Viene riprodotto fino alla fine senza interruzioni.

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

