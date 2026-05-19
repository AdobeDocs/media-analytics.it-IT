---
title: Contenuto principale live
description: Visualizza un esempio di come tracciare il contenuto live utilizzando Media SDK.
uuid: e92e99f4-c395-48aa-8a30-cbdd2f5fc07c
exl-id: f6a00ffd-da6a-4d62-92df-15d119cfc426
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/oOshJZEQmXqgNh5l10-qhLMO8dmph6Tz9mpH0a4FePU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 747
ht-degree: 77%

---

# Contenuto principale live{#live-main-content}

## Scenario {#scenario}

In questo scenario, esiste una risorsa live senza annunci riprodotta per 40 secondi dopo l’unione del flusso live.

| Trigger | metodo Heartbeat | Chiamate di rete | Note   |
|---|---|---|---|
| L’utente fa clic su **[!UICONTROL Play]** | `trackSessionStart` | Inizio contenuto Analytics, inizio contenuto Heartbeat | Questo può essere un clic dell’utente **[!UICONTROL Play]** o un evento di riproduzione automatica. |
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

Ad esempio, supponiamo che un evento di streaming LIVE inizi a mezzanotte e venga eseguito per 24 ore (`a.media.length=86400`; `l:asset:length=86400`). Quindi, supponiamo che un utente inizi a riprodurre lo streaming LIVE a 12:00pm. In questo scenario, devi impostare `l:event:playhead` a 43200 (12 ore dalla mezzanotte UTC di quel giorno in secondi).

### In pausa

Quando un utente mette in pausa la riproduzione, deve essere applicata la stessa logica della “testina di riproduzione live” applicata all&#39;inizio della riproduzione. Quando l’utente ricomincia a riprodurre lo streaming LIVE, è necessario impostare il valore `l:event:playhead` in base al nuovo numero di secondi dalla mezzanotte UTC, _non_ dal punto in cui l’utente ha messo in pausa lo streaming LIVE.

## Tracciamento delle modifiche del programma in un flusso live {#live-program-changes}

Quando un flusso in diretta passa da un programma o una presentazione a un altro (un modello comune per le proprietà di trasmissione e cavo), ogni programma deve essere tracciato come sessione separata. Questo consente di generare rapporti sul coinvolgimento e sul tempo trascorso per singolo titolo, anziché attribuire tutte le visualizzazioni a un singolo flusso continuo.

**Approccio consigliato:**

1. Al termine del programma corrente (o quando il lettore segnala un evento di modifica del programma), chiamare `trackSessionEnd` per chiudere la sessione corrente.
2. Quando inizia il nuovo programma, chiamare `trackSessionStart` con i metadati del nuovo programma (nome, ID, tipo di contenuto e così via).

Il tracciamento di ogni programma come propria sessione mantiene [il tempo di contenuto trascorso](/help/reporting/metrics/content-time-spent.md), [gli indicatori di avanzamento](/help/reporting/metrics/progress-markers.md) e le metriche di completamento definite nell&#39;ambito del singolo programma e consente di creare rapporti accurati sul pubblico per titolo. Utilizza `trackSessionEnd` anziché `trackComplete` per la transizione: `trackComplete` segnala che il visualizzatore ha guardato intenzionalmente la fine di un contenuto discreto, mentre `trackSessionEnd` è corretto qui perché il flusso continua con una programmazione diversa anziché terminare.

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
