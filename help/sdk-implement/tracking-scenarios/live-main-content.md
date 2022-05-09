---
title: 'Contenuto principale live '
description: Visualizza un esempio di come tracciare il contenuto live utilizzando Media SDK.
uuid: e92e99f4-c395-48aa-8a30-cbdd2f5fc07c
exl-id: f6a00ffd-da6a-4d62-92df-15d119cfc426
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 165c7f01a2d2c32df518c89a5c49637107d41086
workflow-type: ht
source-wordcount: '575'
ht-degree: 100%

---

# Contenuto principale live {#live-main-content}

## Scenario {#scenario}

In questo scenario, esiste una risorsa live senza annunci riprodotta per 40 secondi dopo l’unione del flusso live.

| Trigger | metodo Heartbeat | Chiamate di rete | Note   |
|---|---|---|---|
| Clic utente **[!UICONTROL Play]** | `trackSessionStart` | Inizio contenuto Analytics, inizio contenuto Heartbeat | Questo può essere un clic dell’utente su **[!UICONTROL Play]** oppure un evento di riproduzione automatica. |
| Viene riprodotto il primo fotogramma del file multimediale. | `trackPlay` | Riproduzione di contenuti Heartbeat | Questo metodo attiva il timer. Gli heartbeat vengono inviati ogni 10 secondi, a condizione che la riproduzione continui. |
| Il contenuto viene riprodotto. |  | Heartbeat dei contenuti |  |
| La sessione viene terminata. | `trackSessionEnd` |  | `SessionEnd` indica la fine di una sessione di visualizzazione. Questa API deve essere chiamata anche se l’utente non utilizza i file multimediali per il completamento. |

## Parametri {#parameters}

Molti degli stessi valori visualizzati nelle chiamate di avvio dei contenuti di Adobe Analytics vengono visualizzati anche nelle chiamate di avvio dei contenuti di Heartbeat. Visualizzerai anche molti altri parametri utilizzati da Adobe per popolare i vari rapporti multimediali in Adobe Analytics. Non saranno trattati tutti ma solo quelli più importanti.

### Inizio contenuto Heartbeat

| Parametro | Valore | Note |
|---|---|---|
| `s:sc:rsid` | &lt;ID suite di rapporti Adobe> |  |
| `s:sc:tracking_serve` | &lt;URL del server di tracciamento di Analytics> |  |
| `s:user:mid` | `s:user:mid` | Deve corrispondere al valore mid nella chiamata di avvio del contenuto di Adobe Analytics |
| `s:event:type` | “start” |  |
| `s:asset:type` | “main” |  |
| `s:asset:mediao_id` | &lt;Nome contenuto multimediale> |  |
| `s:stream:type` | live |  |
| `s:meta:*` | Opzionale | Metadati personalizzati impostati sull’elemento multimediale |

## Heartbeat dei contenuti {#content-heartbeats}

Durante la riproduzione dei contenuti multimediali, è presente un timer che invia uno o più heartbeat (o ping) ogni 10 secondi per i contenuti principali e ogni secondo per gli annunci. Questi heartbeat contengono informazioni su riproduzione, annunci, buffering e molti altri elementi. Il contenuto esatto di ogni heartbeat va oltre l’ambito di questo documento, la cosa fondamentale da convalidare è che gli heartbeat vengano attivati in modo coerente mentre la riproduzione continua.

Negli heartbeat dei contenuti, cerca alcuni aspetti specifici:

| Parametro | Valore | Note |
|---|---|---|
| `s:event:type` | “play” |  |
| `l:event:playhead` | &lt;posizione testina di riproduzione> ad esempio 50, 60, 70 | Ciò dovrebbe riflettere la posizione attuale della testina di riproduzione. |

## Contenuto Heartbeat completato {#heartbeat-content-complete}

Non ci sarà una chiamata completa in questo scenario, perché il flusso live non è mai stato completato.

## Impostazioni dei valori della testina di riproduzione

Per i flussi LIVE, è necessario impostare il valore della testina di riproduzione come numero di secondi dalla mezzanotte UTC di quel giorno, in modo che nel reporting, gli analisti possano determinare a quale punto gli utenti si uniscono e lasciano il flusso LIVE entro una visualizzazione di 24 ore.

### All’avvio

Per i file multimediali LIVE, quando un utente inizia a riprodurre il flusso, è necessario impostare `l:event:playhead` al numero di secondi dalla mezzanotte UTC di quel giorno. Questo è diverso da VOD, dove la testina di riproduzione è impostata su “0”. Nota: quando si utilizzano i marcatori di avanzamento, è necessario specificare la durata del contenuto e la testina di riproduzione deve essere aggiornata come numero di secondi dall’inizio dell’elemento multimediale, a partire da 0.

Ad esempio, supponiamo che un evento di streaming LIVE inizi a mezzanotte e venga eseguito per 24 ore (`a.media.length=86400`; `l:asset:length=86400`). Quindi, supponiamo che un utente inizi a riprodurre lo streaming LIVE alle 12:00. In questo scenario, devi impostare `l:event:playhead` a 43200 (12 ore dalla mezzanotte UTC di quel giorno in secondi).

### In pausa

Quando un utente mette in pausa la riproduzione, deve essere applicata la stessa logica della “testina di riproduzione live” applicata all&#39;inizio della riproduzione. Quando l’utente ricomincia a riprodurre lo streaming LIVE, è necessario impostare il valore `l:event:playhead` in base al nuovo numero di secondi dalla mezzanotte UTC, _non_ dal punto in cui l’utente ha messo in pausa lo streaming LIVE.

## Codice di esempio {#sample-code}

![](assets/live-content-playback.png)

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

Di seguito è riportato l’ordine di chiamata API previsto:

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
