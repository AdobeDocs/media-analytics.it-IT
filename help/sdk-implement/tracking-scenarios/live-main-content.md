---
title: Contenuto principale live
description: Un esempio di come tenere traccia del contenuto live con Media SDK.
uuid: e92e99f4-c395-48aa-8a30-cbdd2f5fc07c
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Contenuto principale live{#live-main-content}

## Scenario {#scenario}

In questo scenario, dopo l'unione del flusso live è disponibile una risorsa live senza annunci riprodotti per 40 secondi.

| Attivatore | Metodo Heartbeat | Chiamate di rete | Note   |
|---|---|---|---|
| Clic utente **[!UICONTROL Play]** | `trackSessionStart` | Inizio contenuto Analytics, Inizio contenuto Heartbeat | Può trattarsi di un clic dell'utente **[!UICONTROL Play]** o di un evento di riproduzione automatica. |
| Viene riprodotto il primo fotogramma del file multimediale. | `trackPlay` | Heartbeat Content Play | Questo metodo attiva il timer. Gli heartbeat vengono inviati ogni 10 secondi fintanto che la riproduzione continua. |
| Il contenuto viene riprodotto. |  | Heartbeat di contenuto |  |
| La sessione è finita. | `trackSessionEnd` |  | `SessionEnd` indica la fine di una sessione di visualizzazione. Questa API deve essere chiamata anche se l'utente non utilizza il supporto per il completamento. |

## Parametri {#parameters}

Molti degli stessi valori visualizzati nelle chiamate di avvio dei contenuti di Adobe Analytics sono visibili anche nelle chiamate di avvio dei contenuti di Heartbeat. Verranno inoltre visualizzati molti altri parametri utilizzati da Adobe per compilare i vari rapporti sui file multimediali in Adobe Analytics. Non li copriremo tutti qui, solo quelli veramente importanti.

### Avvio contenuto Heartbeat

| Parametro | Valore | Note |
|---|---|---|
| `s:sc:rsid` | &lt;ID suite di rapporti Adobe&gt; |  |
| `s:sc:tracking_serve` | &lt;URL del server di tracciamento Analytics&gt; |  |
| `s:user:mid` | `s:user:mid` | Deve corrispondere al valore mid nella chiamata di avvio contenuto di Adobe Analytics |
| `s:event:type` | "start" |  |
| `s:asset:type` | "main" |  |
| `s:asset:mediao_id` | &lt;Nome file multimediale&gt; |  |
| `s:stream:type` | live |  |
| `s:meta:*` | optional | Metadati personalizzati impostati per il supporto |

## Heartbeat di contenuto {#content-heartbeats}

Durante la riproduzione dei contenuti multimediali, è presente un timer che invia uno o più heartbeat (o ping) ogni 10 secondi per i contenuti principali e ogni secondo per gli annunci. Questi heartbeat contengono informazioni su riproduzione, annunci pubblicitari, buffering e molti altri elementi. Il contenuto esatto di ogni heartbeat va oltre l'ambito di questo documento, la cosa fondamentale da convalidare è che i heartbeat vengono attivati in modo coerente mentre la riproduzione continua.

Nei heartbeat dei contenuti, cercate alcuni punti specifici:

| Parametro | Valore | Note |
|---|---|---|
| `s:event:type` | "play" |  |
| `l:event:playhead` | &lt;posizione dell'indicatore di riproduzione&gt; ad esempio, 50, 60, 70 | Questo deve riflettere la posizione corrente dell'indicatore di riproduzione. |

## Heartbeat Content Complete {#heartbeat-content-complete}

In questo scenario non verrà eseguita una chiamata completa, perché il flusso live non è mai stato completato.

## Impostazioni valore playhead

Per i flussi LIVE, è necessario impostare l'indicatore di riproduzione su un offset a partire dall'inizio della programmazione, in modo che, nel reporting, gli analisti possano determinare a quale punto gli utenti si uniscono e lasciare il flusso LIVE entro una visualizzazione di 24 ore.

### All'inizio

Per i supporti LIVE, quando un utente avvia la riproduzione del flusso, è necessario impostare `l:event:playhead` l'offset corrente, in secondi. Questo è diverso da VOD, dove si imposta la testina di riproduzione su "0".

Ad esempio, supponiamo che un evento di streaming in diretta inizi a mezzanotte e prosegua per 24 ore (`a.media.length=86400`; `l:asset:length=86400`). Quindi, supponiamo che un utente inizi a riprodurre lo streaming LIVE alle 12:00. In questo scenario, impostate `l:event:playhead` su 43200 (12 ore nel flusso).

### In pausa

Quando un utente mette in pausa la riproduzione, deve essere applicata la stessa logica dell'indicatore di riproduzione live applicata all'inizio della riproduzione. Quando l'utente ritorna a riprodurre il flusso LIVE, è necessario impostare il `l:event:playhead` valore sulla nuova posizione dell'indicatore di riproduzione offset, _non_ sul punto in cui l'utente ha messo in pausa il flusso LIVE.

## Codice di esempio {#sample-code}

![](assets/live-content-playback.png)

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

Di seguito è riportato l'ordine di chiamata API previsto:

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

