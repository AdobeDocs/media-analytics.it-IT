---
title: Debug di SDK
description: Scopri le funzioni di tracciamento/registrazione disponibili in Media SDK.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
exl-id: c2de6454-8538-4d07-a099-e278b153d894
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 100%

---

# Debug di SDK {#sdk-debugging}

Puoi abilitare e disabilitare la registrazione. Media SDK fornisce un ampio meccanismo di tracciamento/registrazione in tutto lo stack di tracciamento dei contenuti multimediali. Per abilitare o disabilitare la registrazione, imposta il flag `debugLogging` sull’oggetto Config.

## Codice di esempio per la registrazione di debug

### Android

```java
// Media Heartbeat initialization
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.debugLogging = true;

// Use this space for setting other config values
MediaHeartbeat _heartbeat = new MediaHeartbeat(this, config);
```

### iOS

```
// Media Heartbeat Initialization
ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];
config.debugLogging = YES;

// Use this space for setting other config values
ADBMediaHeartbeat *_mediaHeartbeat =  
[[ADBMediaHeartbeat alloc] initWithDelegate:self config:config];
```

### JavaScript

```js
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.debugLogging = true;
this._mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

### OTT (Chromecast, Roku)

La libreria ADBMobile fornisce la registrazione di debug attraverso il metodo `setDebugLogging`. La registrazione di debug deve essere impostata su `false` per tutte le app di produzione.

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

## Messaggi di registro

I messaggi di registro seguono questo formato:

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>]
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **timestamp:** ora corrente della CPU (fuso orario per GMT)
* **livello:** sono definiti 4 livelli di messaggio:
   * INFO: di solito i dati di input dall’applicazione (convalida nome del lettore, ID video, ecc.)
   * DEBUG: registri di debug, utilizzati dagli sviluppatori per eseguire il debug di problemi più complessi
   * AVVERTENZA: indica potenziali errori di integrazione/configurazione o bug dell’SDK Heartbeat
   * ERRORE: indica errori importanti di integrazione o bug dell’SDK Heartbeat
* **tag:** nome del sottocomponente che ha emesso il messaggio di registro (in genere il nome della classe)
* **messaggio:** messaggio di traccia effettivo

Puoi utilizzare l’output dei registri dalla libreria Media SDK per verificare l’implementazione. Una buona strategia è quella di cercare tra i registri la stringa `#track`. Questo metterà in evidenza tutte le chiamate `track*()` effettuate dall’applicazione.

Per esempio, i registri filtrati per `#track` potrebbero essere simili al seguente:

```js
[16:10:29 GMT­0700 (PDT).222] [INFO] [plugin::player] #trackVideoLoad()
[16:10:29 GMT­0700 (PDT).230] [INFO] [plugin::player] #trackSessionStart()
[16:10:29 GMT­0700 (PDT).250] [INFO] [plugin::player] #trackPlay()
[16:10:29 GMT­0700 (PDT).759] [INFO] [plugin::player] #trackChapterStart()
[16:10:44 GMT­0700 (PDT).769] [INFO] [plugin::player] #trackAdStart()
[16:10:59 GMT­0700 (PDT).752] [INFO] [plugin::player] #trackAdComplete()
[16:10:59 GMT­0700 (PDT).770] [INFO] [plugin::player] #trackChapterStart()
[16:11:29 GMT­0700 (PDT).734] [INFO] [plugin::player] #trackPause()
[16:11:29 GMT­0700 (PDT).764] [INFO] [plugin::player] #trackComplete()
[16:11:29 GMT­0700 (PDT).766] [INFO] [plugin::player] #trackVideoUnload()
```
