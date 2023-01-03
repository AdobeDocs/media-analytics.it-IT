---
title: Riproduzione VOD senza annunci
description: Visualizza un esempio di tracciamento della riproduzione VOD che non contiene annunci.
uuid: ee2a1b79-2c2f-42e1-8e81-b62bbdd0d8cb
exl-id: 9e2240f0-da8d-4dcc-9d44-0f121c60d924
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '364'
ht-degree: 100%

---

# Riproduzione VOD senza annunci {#vod-playback-with-no-ads}

## Scenario {#scenario}

Questo scenario ha una risorsa VOD, senza annunci, che viene riprodotto una volta dall’inizio alla fine.

| Trigger | metodo Heartbeat | Chiamate di rete | Note   |
|---|---|---|---|
| Clic utente **[!UICONTROL Play]** | `trackSessionStart` | Inizio contenuto Analytics, inizio contenuto Heartbeat | Questo può essere un utente che fa clic su Play o un evento di riproduzione automatica. |
| Primo fotogramma del supporto | `trackPlay` | Riproduzione di contenuti Heartbeat | Questo metodo attiva il timer e da questo momento in poi gli heartbeat verranno inviati ogni 10 secondi per la durata della riproduzione. |
| Riproduzione dei contenuti |  | Heartbeat dei contenuti |  |
| Contenuto completato | `trackComplete` | Contenuto Heartbeat completato | *Completato* significa che è stata raggiunta la fine del playhead. |

## Parametri {#parameters}

Molti degli stessi valori visualizzati nelle chiamate di avvio dei contenuti Heartbeat sono visibili anche nelle chiamate `Content Start` di Adobe Analytics. Esistono molti parametri utilizzati da Adobe per compilare i vari rapporti multimediali, ma solo i parametri più importanti sono elencati nella tabella seguente:

### Inizio contenuto Heartbeat

| Parametro | Valore | Note   |
|---|---|---|
| `s:sc:rsid` | &lt;ID suite di rapporti Adobe> |  |
| `s:sc:tracking_server` | &lt;URL del server di tracciamento di Analytics> |  |
| `s:user:mid` | deve essere impostato | Deve corrispondere al valore mid nella chiamata `Adobe Analytics Content Start`. |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:media_id` | &lt;Nome contenuto multimediale> |  |
| `s:meta:*` | Opzionale | Metadati personalizzati impostati sul supporto. |

## Riproduzione di contenuti Heartbeat {#heartbeat-content-play}

Questi parametri dovrebbero avere un aspetto quasi identico alla chiamata `Heartbeat Content Start`, ma la differenza chiave è il parametro `s:event:type`. Tutti gli altri parametri devono ancora esistere.

| Parametro | Valore | Note   |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |

## Heartbeat dei contenuti {#content-heartbeats}

Durante la riproduzione dei contenuti multimediali, un timer invia almeno un heartbeat ogni 10 secondi. Questi heartbeat contengono informazioni su riproduzione, annunci pubblicitari, buffering e così via. Il contenuto esatto di ogni heartbeat va oltre l’ambito di questo documento, ma il problema fondamentale è che gli heartbeat vengono attivati in modo coerente mentre la riproduzione continua.

Negli heartbeat di contenuto, cerca i seguenti parametri:

| Parametri | Valore | Note   |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | &lt;posizione testina di riproduzione> ad esempio 50,60,70 | Questo parametro riflette la posizione corrente della testina di riproduzione. |

## Contenuto Heartbeat completato {#heartbeat-content-complete}

Una volta completata la riproduzione, cioè quando viene raggiunta la fine della testina di riproduzione, viene inviata una chiamata `Heartbeat Content Complete`. Questa chiamata assomiglia ad altre chiamate Heartbeat, ma contiene alcuni parametri specifici:

| Parametri | Valore | Note   |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

## Codice di esempio {#sample-code}

In questo caso, il contenuto è lungo 40 secondi. Viene riprodotto fino alla fine senza interruzioni.

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
