---
seo-title: Contenuto principale live
title: Contenuto principale live
uuid: e 92 e 99 f 4-c 395-48 aa -8 a 30-cbdd 2 f 5 fc 07 c
translation-type: tm+mt
source-git-commit: 9dbd621e10ba198b9331e5a7579fcbd3b6173ecd

---


# Live main content{#live-main-content}

## Scenario {#section_13BD203CBF7546D2A6AD0129B1EEB735}

In questo scenario, esiste una risorsa live senza annunci pubblicitari per 40 sec dopo aver partecipato al flusso live.

| Attivatore | Heartbeat, metodo | Chiamate di rete | Note   |
|---|---|---|---|
| User clicks **[!UICONTROL Play]** | `trackSessionStart` | Inizio del contenuto di Analytics, Inizio contenuto Heartbeat | This can be a user clicking **[!UICONTROL Play]** or an auto-play event. |
| Viene riprodotto il primo fotogramma del supporto. | `trackPlay` | Riproduzione contenuto heartbeat | Questo metodo attiva il timer. Heartbeats viene inviato ogni 10 secondi a condizione che la riproduzione continui. |
| Il contenuto viene riprodotto. |  | Heartbeats contenuto |  |
| La sessione è terminata. | `trackSessionEnd` |  | `SessionEnd` indica la fine di una sessione di visualizzazione. Questa API deve essere chiamata anche se l'utente non utilizza il supporto per il completamento. |

## Parametri {#section_D52B325B99DA42108EF560873907E02C}

Molti degli stessi valori disponibili sulle chiamate di avvio del contenuto di Adobe Analytics visualizzeranno anche On Heartbeat Content Start Calls. Vedrai anche molti altri parametri utilizzati da Adobe per comporre i vari rapporti Contenuti multimediali in Adobe Analytics. Non li copriremo qui, ma solo quelli davvero importanti.

### Inizio contenuto heartbeat

| Parametro | Valore | Note |
|---|---|---|
| `s:sc:rsid` | &lt; ID suite di rapporti &gt; |  |
| `s:sc:tracking_serve` | &lt; URL del server di tracciamento Analytics &gt; |  |
| `s:user:mid` | `s:user:mid` | Deve corrispondere al valore mid in Adobe Analytics Content Start Call |
| `s:event:type` | " start " |  |
| `s:asset:type` | " main " |  |
| `s:asset:mediao_id` | &lt; Nome file multimediali &gt; |  |
| `s:stream:type` | live |  |
| `s:meta:*` | facoltativo | Set di metadati personalizzati sul supporto |

## Content Heartbeats {#section_7B387303851A43E5993F937AE2B146FE}

Durante la riproduzione di contenuti multimediali, è presente un timer che invierà uno o più heartbebeat ogni 10 secondi. Tali heartbeat contengono informazioni su riproduzione, annunci pubblicitari, buffering e molti altri elementi. Il contenuto esatto di ogni heartbeat va oltre l'ambito di questo documento, il punto critico da convalidare è che i heartbeat vengono attivati in modo coerente mentre la riproduzione continua.

Nei heartbeat del contenuto, cerca alcuni elementi specifici:

| Parametro | Valore | Note |
|---|---|---|
| `s:event:type` | "play" |  |
| `l:event:playhead` | &lt; posizione della linea di scansione &gt;, ad esempio 50, 60, 70 | Deve riflettere la posizione corrente dell'indicatore di riproduzione. |

## Heartbeat Content Complete {#section_2CA970213AF2457195901A93FC9D4D0D}

In questo scenario non sarà più disponibile una chiamata completa, in quanto il flusso live non è mai stato completato.

## Impostazioni valore playhead

Per i flussi LIVE, è necessario impostare l'indicatore di riproduzione su un offset dall'avvio della programmazione, in modo che in reporting gli analisti possano determinare in quali punti gli utenti entrano e escono dal flusso LIVE entro una visualizzazione di 24 ore.

### All'inizio

For LIVE media, when a user starts playing the stream, you need to set `l:event:playhead` to the current offset, in seconds. Ciò si trova invece di VOD, dove si imposta l'indicatore di riproduzione su "0".

For example, say a LIVE streaming event starts at midnight and runs for 24 hours (`a.media.length=86400`; `l:asset:length=86400`). Quindi, supponiamo che un utente inizi a riprodurre lo streaming LIVE alle 12:00. In this scenario, you should set `l:event:playhead` to 43200 (12 hours into the stream).

### Pausa

La stessa logica di riproduzione live applicata all'inizio della riproduzione deve essere applicata quando un utente mette in pausa la riproduzione. When the user returns to playing the LIVE stream, you must set the `l:event:playhead` value to the new offset playhead position, _not_ to the point where the user paused the LIVE stream.

## Codice di esempio {#section_vct_j2j_x2b}

![](assets/live-content-playback.png)

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
//    i.e., there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen. 
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since the user does not watch live media to completion, there  
//    is no need to call trackComplete().  
_mediaHeartbeat.trackSessionEnd(); 
....... 
....... 
```

### App

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
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 3. Call trackSessionEnd when user ends the playback session. Since the user  
//    does not watch live media to completion, there is no need to call  
//    trackComplete. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript

Ecco il previsto ordine delle chiamate API:

```js
// Set up mediaObject 
var mediaInfo =  
MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME,  
                                 Configuration.MEDIA_ID,  
                                 Configuration.MEDIA_LENGTH,  
                                 MediaHeartbeat.StreamType.VOD); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay  
//    is used, i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since user does not watch live media to completion, there is  
//    no need to call trackComplete(). 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

