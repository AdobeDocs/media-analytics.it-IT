---
title: Riferimento API di JavaScript 3.x Media SDK
description: Riferimento API per Media SDK JavaScript 3.x (classi ADB.Media e ADB.MediaConfig).
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3f8a2b5-1d4e-4f9a-8c7b-3a2d1f0e9b6c
source-git-commit: 1022e0851d58db0c9b523ebb7b52d379239a2e07
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 17%

---


# Riferimento API di JavaScript 3.x Media SDK

>[!BEGINSHADEBOX]

Questa pagina descrive il SDK JavaScript 3.x solo per Analytics. Per l&#39;implementazione consigliata, vedere [Implementare Streaming Media utilizzando Edge Network](/help/implementation/edge/edge-web-sdk.md).

>[!ENDSHADEBOX]

## ADB.Media

### Metodi statici

+++configure

Configura MediaSDK per il tracciamento. Questo metodo deve essere chiamato una volta prima di creare qualsiasi istanza di tracciamento in una pagina.

**Sintassi**

```javascript
ADB.Media.configure(mediaConfig, appMeasurement);
```

| Nome variabile | Tipo | Descrizione |
|---|---|---|
| `mediaConfig` | `ADB.MediaConfig` | Configurazione supporto valida |
| `appMeasurement` | oggetto | istanza AppMeasurement |

**Esempio**

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

+++

+++getInstance

Crea un&#39;istanza del file multimediale per tenere traccia della sessione di riproduzione. Restituisce `null` se chiamato prima della configurazione del supporto.

**Sintassi**

```javascript
ADB.Media.getInstance(trackerConfig)
```

| Nome variabile | Tipo | Obbligatorio | Descrizione |
| :--- | :--- | :---: | :--- |
| `trackerConfig` | Configurazione del tracker | No | Oggetto di configurazione del tracker. |

**Esempio**

```javascript
var tracker = ADB.Media.getInstance();
```

Per eseguire l&#39;override di `channel` o `playerName` per istanza di tracciamento, passare i valori di override nell&#39;oggetto di configurazione del tracciatore.

**Esempio con configurazione del tracker**

```javascript
const trackerConfig = {
  [Media.TrackerConfig.Channel]: "custom_channel_name",
  [Media.TrackerConfig.PlayerName]: "custom_player_name",
}
this._mediaTracker = Media.getInstance(trackerConfig);
```

+++

+++createMediaObject

Crea un oggetto contenente informazioni multimediali. Restituisce un oggetto vuoto se vengono passati parametri non validi.

**Sintassi**

```javascript
ADB.Media.createMediaObject(name, id, length, streamType, mediaType)
```

| Nome variabile | Tipo | Descrizione |
| :--- | :--- | :--- |
| `name` | stringa | Stringa non vuota che indica il nome del file multimediale |
| `id` | string | Stringa non vuota che denota un identificatore multimediale univoco |
| `length` | numero | Numero positivo che indica la lunghezza del file multimediale in secondi. Usa `0` se la lunghezza è sconosciuta. |
| `streamType` | string | Tipo di flusso o stringa non vuota per indicare il tipo di flusso multimediale. |
| `mediaType` | Tipo di file multimediale | Tipo di file multimediale (audio o video) |

**Esempio**

```javascript
var mediaObject = ADB.Media.createMediaObject("video-name",
                                              "video-id",
                                              60.0,
                                              ADB.Media.StreamType.VOD,
                                              ADB.Media.MediaType.Video);
```

+++

+++createAdBreakObject

Crea un oggetto contenente informazioni sull&#39;interruzione. Restituisce un oggetto vuoto se vengono passati parametri non validi.

**Sintassi**

```javascript
ADB.Media.createAdBreakObject(name, position, startTime);
```

| Nome variabile | Tipo | Descrizione |
| :--- | :--- | :--- |
| `name` | stringa | Stringa non vuota che indica il nome dell’interruzione (pre-roll, mid-roll e post-roll) |
| `position` | numero | La posizione numerica dell’interruzione pubblicitaria all’interno del contenuto, a partire da 1 |
| `startTime` | numero | Valore della testina di riproduzione all’inizio dell’interruzione pubblicitaria. |

**Esempio**

```javascript
var adbreakObject = ADB.Media.createAdBreakObject("midroll", 2, 30.0);
```

+++

+++createAdObject

Crea un oggetto contenente informazioni sull’annuncio. Restituisce un oggetto vuoto se vengono passati parametri non validi.

**Sintassi**

```javascript
ADB.Media.createAdObject(name, id, position, length);
```

| Nome variabile | Tipo | Descrizione |
| :--- | :--- | :--- |
| `name` | stringa | Stringa non vuota che denota il nome dell’annuncio |
| `id` | string | Stringa non vuota che denota l’ID annuncio |
| `position` | numero | La posizione numerica dell’annuncio all’interno dell’interruzione, a partire da 1 |
| `length` | numero | Numero positivo che indica la lunghezza dell’annuncio |

**Esempio**

```javascript
var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0)
```

+++

+++createChapterObject

Crea un oggetto contenente informazioni sul capitolo. Restituisce un oggetto vuoto se vengono passati parametri non validi.

**Sintassi**

```javascript
ADB.Media.createChapterObject(name, position, length, startTime)
```

| Nome variabile | Tipo | Descrizione |
| :--- | :--- | :--- |
| `name` | stringa | Stringa non vuota che denota il nome del capitolo |
| `position` | numero | La posizione del capitolo all’interno del contenuto, a partire da 1 |
| `length` | numero | Numero positivo che indica la lunghezza del capitolo |
| `startTime` | numero | Valore della testina di riproduzione all’inizio del capitolo |

**Esempio**

```javascript
var chapterObject = ADB.Media.createChapterObject("name", 1, 30.0, 0)
```

+++

+++createStateObject

Crea un oggetto contenente informazioni sullo stato. Restituisce un oggetto vuoto se vengono passati parametri non validi.

**Sintassi**

```javascript
ADB.Media.createStateObject(name)
```

| Nome variabile | Tipo | Descrizione |
| :--- | :--- | :--- |
| `name` | stringa | Stato del lettore o stringa non vuota che indica il nome dello stato |

**Esempio**

```javascript
var stateObject = ADB.Media.createStateObject("customstate");
```

+++

+++createQoEObject

Crea un oggetto contenente informazioni QoE. Restituisce un oggetto vuoto se vengono passati parametri non validi.

**Sintassi**

```javascript
ADB.Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)
```

| Nome variabile | Tipo | Descrizione |
| :--- | :--- | :--- |
| `bitrate` | numero | Numero positivo che indica il bitrate corrente (0 se sconosciuto) |
| `startupTime` | numero | Numero positivo che indica il tempo di avvio (0 se sconosciuto) |
| `fps` | numero | Numero positivo che indica fps correnti (0 se sconosciuto) |
| `droppedFrames` | numero | Numero positivo che indica il numero di fotogrammi saltati (0 se sconosciuto) |

**Esempio**

```javascript
qoeObject = ADB.Media.createQoEObject(10000000, 2, 23, 10);
```

+++

+++version

Restituisce la versione MediaSDK.

**Sintassi**

```javascript
ADB.Media.version
```

**Esempio**

```javascript
console.log(ADB.Media.version);
```

+++

### Metodi di istanza

+++trackSessionStart

Traccia l’intenzione di inizio riproduzione. Viene avviata una sessione di tracciamento sull’istanza di tracciamento dei contenuti multimediali. Vedi anche Ripresa file multimediale.

**Sintassi**

```javascript
ADB.Media.trackSessionStart(mediaObject, contextData);
```

| Nome variabile | Descrizione | Obbligatorio |
| :--- | :--- | :---: |
| `mediaObject` | Informazioni multimediali create utilizzando il metodo `createMediaObject`. | Sì |
| `contextData` | Dati contestuali multimediali facoltativi. Per le chiavi di metadati standard, utilizza costanti video standard o costanti audio standard. | No |

**Esempio**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[ADB.Media.VideoMetadataKeys.Show] = "Sample Show";
contextData["isUserLoggedIn"] = "false";
contextData["tvStation"] = "Sample TV Station";

tracker.trackSessionStart(mediaObject, contextData);
```

+++

+++trackPlay

Tracciare la riproduzione o la ripresa di contenuti multimediali dopo una pausa precedente.

**Sintassi**

```javascript
ADB.Media.trackPlay();
```

**Esempio**

```javascript
tracker.trackPlay();
```

+++

+++trackPause

Tracciare la pausa dei contenuti multimediali.

**Sintassi**

```javascript
ADB.Media.trackPause();
```

**Esempio**

```javascript
tracker.trackPause();
```

+++

+++trackComplete

Tracciamento del contenuto multimediale completato. Chiama questo metodo solo quando il contenuto multimediale è stato completamente visualizzato.

**Sintassi**

```javascript
ADB.Media.trackComplete();
```

**Esempio**

```javascript
tracker.trackComplete();
```

+++

+++trackSessionEnd

Tracciare la fine di una sessione di visualizzazione. Chiama questo metodo anche se l’utente non visualizza il contenuto multimediale fino al completamento.

**Sintassi**

```javascript
ADB.Media.trackSessionEnd();
```

**Esempio**

```javascript
tracker.trackSessionEnd();
```

+++

+++trackError

Tracciare un errore nella riproduzione di contenuti multimediali.

**Sintassi**

```javascript
ADB.Media.trackError(errorId);
```

| Nome variabile | Descrizione | Obbligatorio |
| :--- | :--- | :---: |
| `errorId` | Stringa non vuota contenente informazioni sull’errore | Sì |

**Esempio**

```javascript
tracker.trackError("errorId");
```

+++

+++trackEvent

Metodo per tenere traccia degli eventi multimediali.

| Nome variabile | Descrizione |
| :--- | :--- |
| `event` | Evento multimediale |
| `info` | Per l&#39;evento `AdBreakStart`, le informazioni sull&#39;interruzione vengono create utilizzando il metodo `createAdBreakObject`. Per l&#39;evento `AdStart`, le informazioni sull&#39;annuncio vengono create utilizzando il metodo `createAdObject`. Per l&#39;evento `ChapterStart`, le informazioni sul capitolo vengono create utilizzando il metodo `createChapterObject`. Per gli eventi `StateStart` e `StateEnd`, le informazioni sullo stato vengono create utilizzando il metodo `createStateObject`. Questo non è richiesto per altri eventi. |
| `contextData` | È possibile fornire dati contestuali facoltativi per `AdStart` e `ChapterStart` eventi. Questo non è richiesto per altri eventi. |

**Sintassi**

```javascript
ADB.Media.trackEvent(event, info, contextData);
```

**Esempi**

**Tracciamento AdBreaks**

```javascript
// AdBreakStart
  var adBreakObject = ADB.Media.createAdBreakObject("preroll", 1, 0)
  tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);

// AdBreakComplete
  tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
```

**Tracciamento annunci**

```javascript
// AdStart
  var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0);

  var adMetadata = {};
  // Standard metadata keys provided by adobe.
  adMetadata[ADB.Media.AdMetadataKeys.Advertiser]  ="Sample Advertiser";
  adMetadata[ADB.Media.AdMetadataKeys.CampaignId] = "Sample Campaign";
  // Custom metadata keys
  adMetadata["affiliate"] = "Sample affiliate";

  tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);

// AdComplete
  tracker.trackEvent(ADB.Media.Event.AdComplete);

// AdSkip
  tracker.trackEvent(ADB.Media.Event.AdSkip);
```

**Tracciamento capitoli**

```javascript
// ChapterStart
  var chapterObject = ADB.Media.createChapterObject("chapter-name", 1, 60.0, 15.0);

  var chapterMetadata = {};
  chapterMetadata["segmentType"] = "Sample segment type";

  tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);

// ChapterComplete
  tracker.trackEvent(ADB.Media.Event.ChapterComplete);

// ChapterSkip
  tracker.trackEvent(ADB.Media.Event.ChapterSkip);
```

**Tracciamento degli stati**

```javascript
// StateStart (ex: Mute is switched on)
  var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
  tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);

// StateEnd (ex: Mute is switched off)
  tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```

**Tracciamento degli eventi di riproduzione**

```javascript
// BufferStart
  tracker.trackEvent(ADB.Media.Event.BufferStart);

// BufferComplete
  tracker.trackEvent(ADB.Media.Event.BufferComplete);

// SeekStart
  tracker.trackEvent(ADB.Media.Event.SeekStart);

// SeekComplete
  tracker.trackEvent(ADB.Media.Event.SeekComplete);
```

**Rilevamento delle modifiche del bitrate**

```javascript
// If the new bitrate value is available provide it to the tracker.
  var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
  tracker.updateQoEObject(qoeObject);

// Bitrate change
  tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

+++

+++updatePlayhead

Fornisci la testina di riproduzione corrente al tracciatore dei contenuti multimediali. Per un tracciamento accurato, chiama questo metodo ogni volta che la testina di riproduzione cambia durante la riproduzione.

**Sintassi**

```javascript
ADB.Media.updatePlayhead(time);
```

| Nome variabile | Descrizione |
| :--- | :--- |
| `time` | Testina di riproduzione corrente in secondi. Per il video on-demand (VOD), il valore è specificato in secondi dall’inizio dell’elemento multimediale. Per lo streaming live, se il lettore non fornisce informazioni sulla durata del contenuto, il valore può essere specificato come il numero di secondi trascorsi dalla mezzanotte UTC di quel giorno. Nota: quando si utilizzano i marcatori di avanzamento, è necessario specificare la durata del contenuto e la testina di riproduzione deve essere aggiornata come numero di secondi dall’inizio dell’elemento multimediale, a partire da 0. |

**Esempio**

```javascript
tracker.updatePlayhead(13.3);

// For live streams
var UTCTimeInSeconds = Math.floor(Date.now() / 1000)
var timeFromMidnightInSecond = UTCTimeInSeconds % 86400

tracker.updatePlayhead(timeFromMidnightInSecond);
```

+++

+++updateQoEObject

Fornisce le informazioni QoE correnti al tracciatore multimediale. Per un tracciamento accurato, chiama questo metodo più volte quando il lettore multimediale fornisce le informazioni QoE aggiornate.

**Sintassi**

```javascript
ADB.Media.updateQoEObject(qoeObject);
```

| Nome variabile | Descrizione |
| :--- | :--- |
| `qoeObject` | Informazioni QoE correnti create utilizzando il metodo `createQoEObject`. |

**Esempio**

```javascript
var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
tracker.updateQoEObject(qoeObject);
```

+++

+++distruggere

Elimina l&#39;istanza di tracciamento.

**Sintassi**

```javascript
ADB.Media.destroy();
```

**Esempio**

```javascript
tracker.destroy();
```

+++

### Costanti

+++Configurazione tracker

Definisce le chiavi di configurazione che possono essere impostate per ogni istanza di tracciamento.

```javascript
ADB.Media.TrackerConfig = {
  Channel: "media.channel",
  PlayerName: "media.playerName"
}
```

+++

+++Tipo di file multimediale

Definisce il tipo di supporto attualmente tracciato.

```javascript
ADB.Media.MediaType = {
  Video: "video",
  Audio: "audio"
}
```

+++

+++Tipo di flusso

Definisce il tipo di flusso del contenuto attualmente tracciato.

```javascript
ADB.Media.StreamType = {
  VOD: "vod",
  Live: "live",
  Linear: "linear",
  Podcast: "podcast",
  Audiobook: "audiobook",
  AOD: "aod"
}
```

+++

+++Chiavi metadati standard

`ADB.Media.VideoMetadataKeys`, `ADB.Media.AudioMetadataKeys` e `ADB.Media.AdMetadataKeys` forniscono le stringhe chiave dei dati di contesto per i metadati standard. Per l&#39;elenco completo delle chiavi e delle corrispondenti variabili di reporting, vedere [Riferimento variabile metadati standard](/help/implementation/variables/standard-metadata/show.md).

+++

+++Eventi multimediali

Definisce il tipo di un evento di tracciamento.

```javascript
ADB.Media.Event = {
  AdBreakStart: "adBreakStart",
  AdBreakComplete: "adBreakComplete",
  AdStart: "adStart",
  AdComplete: "adComplete",
  AdSkip: "adSkip",
  ChapterStart: "chapterStart",
  ChapterComplete: "chapterComplete",
  ChapterSkip: "chapterSkip",
  SeekStart: "seekStart",
  SeekComplete: "seekComplete",
  BufferStart: "bufferStart",
  BufferComplete: "bufferComplete",
  BitrateChange: "bitrateChange",
  StateStart: "stateStart",
  StateEnd: "stateEnd"
}
```

+++

+++Stati del lettore

Definisce i valori standard per il tracciamento dello stato del lettore.

```javascript
ADB.Media.PlayerState = {
  FullScreen: "fullScreen",
  ClosedCaption: "closedCaptioning",
  Mute: "mute",
  PictureInPicture: "pictureInPicture",
  InFocus: "inFocus"
}
```

+++

+++Ripresa file multimediale

Costante per indicare che la sessione di tracciamento corrente sta riprendendo una sessione precedentemente chiusa. Queste informazioni devono essere fornite all’avvio di una sessione di tracciamento.

**Sintassi**

```javascript
ADB.Media.MediaObjectKey = {
  MediaResumed: "resumed"
}
```

**Esempio**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

mediaObject[ADB.Media.MediaObjectKey.MediaResumed] = true;

tracker.trackSessionStart(mediaObject);
```

+++

## ADB.MediaConfig

| Chiave | Obbligatorio | Descrizione |
| :--- | :--- | :--- |
| `trackingServer` | Sì | Digita il nome del server API di raccolta multimediale a cui devono essere inviati i dati di tracciamento dei contenuti multimediali scaricati. Per ricevere queste informazioni, contatta il rappresentante del tuo account Adobe. |
| `channel` | No | Proprietà nome canale |
| `playerName` | No | Nome del lettore multimediale in uso |
| `appVersion` | No | Digita la versione dell’applicazione lettore multimediale/SDK |
| `debugLogging` | No | Attiva o disattiva i registri di Media SDK (valore predefinito: `false`) |
| `ssl` | No | Invia ping su SSL (valore predefinito: `true`) |
