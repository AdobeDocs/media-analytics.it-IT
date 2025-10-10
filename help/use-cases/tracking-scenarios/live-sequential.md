---
title: 'Contenuto principale live con tracciamento sequenziale '
description: Visualizza un esempio di come tracciare il contenuto live con il tracciamento sequenziale utilizzando Media SDK.
uuid: b03477b6-9be8-4b67-a5a0-4cef3cf262ab
exl-id: 277a72b8-453b-41e5-b640-65c43587baf8
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 100%

---

# Contenuto principale live con tracciamento sequenziale {#live-main-content-with-sequential-tracking}

## Scenario {#scenario}

In questo scenario, esiste una risorsa live senza annunci riprodotta per 40 secondi dopo l’unione del flusso live.

Questo è lo stesso scenario della [riproduzione VOD senza annunci](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md), ma una parte del contenuto viene eliminata e una ricerca viene completata da un punto del contenuto principale a un altro punto.

| Trigger | metodo Heartbeat |  Chiamate di rete  |  Note   |
| --- | --- | --- | --- |
| L’utente fa clic su [!UICONTROL Play] | trackSessionStart | Inizio contenuto Analytics, inizio contenuto Heartbeat | La libreria di misurazione non è a conoscenza dell’esistenza di un annuncio pre-roll, pertanto queste chiamate di rete sono identiche allo scenario [riproduzione VOD senza annunci](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md). |
| Viene riprodotto il primo fotogramma del contenuto. | trackPlay | Riproduzione di contenuti Heartbeat | Quando il contenuto del capitolo viene riprodotto prima del contenuto principale, gli heartbeat partono all’inizio del capitolo. |
| Riproduzione dei contenuti | | Heartbeat dei contenuti | Questa chiamata di rete è esattamente la stessa dello scenario [riproduzione VOD senza annunci](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md). |
| Sessione1 terminata (Episodio1 finito) | trackComplete / trackSessionEnd | Contenuto Heartbeat completato | Completata significa che la sessione1 del primo episodio è stata raggiunta e guardata completamente. Prima di iniziare la sessione dell’episodio successivo, questa sessione deve essere terminata. |
| Episodio2 avviato (inizio Sessione2) | trackSessionStart | Avvio contenuto Analytics avvio contenuto Heartbeat | Questo perché l’utente ha visto il primo episodio e ha continuato a guardare un altro episodio |
| 1° fotogramma dell’elemento multimediale | trackPlay | Riproduzione di contenuti Heartbeat | Questo metodo attiva il timer e da questo momento in poi, gli heartbeat verranno inviati ogni 10 secondi, a condizione che la riproduzione continui. |
| Riproduzione dei contenuti | | Heartbeat dei contenuti | |
| Sessione terminata (Episodio2 finito) | trackComplete / trackSessionEnd | Contenuto Heartbeat completato | Completa significa che la Sessione2 del secondo episodio è stata raggiunta e guardata completamente. Prima di iniziare la sessione dell’episodio successivo, questa sessione deve essere terminata. |

## Parametri {#parameters}

### Inizio contenuto Heartbeat

| Parametro | Valore | Note |
|---|---|---|
| `s:sc:rsid` | &lt;ID suite di rapporti Adobe> |  |
| `s:sc:tracking_serve` | &lt;URL del server di tracciamento di Analytics> |  |
| `s:user:mid` | `s:user:mid` | Deve corrispondere al valore mid nella chiamata di avvio del contenuto di Adobe Analytics |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:media_id` | &lt;Nome contenuto multimediale> |  |
| `s:stream:type` | `live` |  |
| `s:meta:*` | *facoltativo* | Metadati personalizzati impostati sull’elemento multimediale |

## Riproduzione di contenuti Heartbeat {#heartbeat-content-play}

Questo dovrebbe assomigliare quasi esattamente alla chiamata di avvio del contenuto Heartbeat, ma con la differenza chiave nel parametro “s:event:type”. Qui devono essere ancora presenti tutti i parametri.

| Parametro | Valore | Note |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |

## Heartbeat dei contenuti {#content-heartbeats}

Durante la riproduzione dei contenuti multimediali, è presente un timer che invia uno o più heartbeat ogni 10 secondi per i contenuti principali e ogni secondo per gli annunci. Questi heartbeat contengono informazioni su riproduzione, annunci, buffering e molti altri elementi. Il contenuto esatto di ogni heartbeat va oltre l’ambito di questo documento, la cosa fondamentale da convalidare è che gli heartbeat vengano attivati in modo coerente mentre la riproduzione continua.

Negli heartbeat dei contenuti, cerca alcuni aspetti specifici:

| Parametro | Valore | Note |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | &lt;posizione testina di riproduzione> ad esempio 50, 60, 70 | Ciò dovrebbe riflettere la posizione attuale della testina di riproduzione. |

## Contenuto Heartbeat completato {#heartbeat-content-complete}

Al termine della riproduzione di un dato episodio (la testina di riproduzione attraversa il limite degli episodi), viene inviata una chiamata a completamento del contenuto di Heartbeat. Questa assomiglia ad altre chiamate Heartbeat, ma contiene un paio di cose specifiche:

| Parametro | Valore | Note |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

## Codice di esempio {#sample-code}

![](assets/ios-live-noads-multiplesessions.png)

### Android

Di seguito è riportato l’ordine di chiamata API previsto:

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

Di seguito è riportato l’ordine di chiamata API previsto:

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

Di seguito è riportato l’ordine di chiamata API previsto:

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
