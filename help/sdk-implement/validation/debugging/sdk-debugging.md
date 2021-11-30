---
title: Debug di SDK
description: Scopri le funzioni di tracciamento/registrazione disponibili in Media SDK.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
exl-id: c2de6454-8538-4d07-a099-e278b153d894
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 819f4a7035e5d9704d17abce6a7cd4c607b7ce39
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 2%

---

# Debug dell’SDK{#sdk-debugging}

Puoi abilitare e disabilitare la registrazione. Media SDK fornisce un ampio meccanismo di tracciamento/registrazione in tutto lo stack di tracciamento dei contenuti multimediali. Per abilitare o disabilitare la registrazione, imposta la `debugLogging` Flag sull&#39;oggetto Config.

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

La libreria ADBMobile fornisce la registrazione di debug attraverso `setDebugLogging` metodo . La registrazione di debug deve essere impostata su `false` per tutte le app di produzione.

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

## Messaggi di registro

I messaggi di log seguono questo formato:

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>]
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **timestamp:** Ora corrente della CPU (fuso orario per GMT)
* **livello:** Sono definiti 4 livelli di messaggio:
   * INFO - Di solito i dati di input dall&#39;applicazione (convalidare il nome del lettore, l&#39;ID video, ecc.)
   * DEBUG - Log di debug, utilizzati dagli sviluppatori per eseguire il debug di problemi più complessi
   * AVVERTENZA: indica potenziali errori di integrazione/configurazione o bug dell&#39;SDK Heartbeat
   * ERRORE - Indica errori importanti di integrazione o bug dell&#39;SDK per Heartbeat
* **tag:** Nome del sottocomponente che ha emesso il messaggio di log (in genere il nome della classe)
* **messaggio:** Messaggio di traccia effettivo

Puoi utilizzare l’output dei registri dalla libreria Media SDK per verificare l’implementazione. Una buona strategia è quella di cercare tra i log la stringa `#track`. Questo metterà in evidenza tutte le `track*()` chiamate effettuate dall&#39;applicazione.

Per esempio, questo è ciò per cui i log filtrano `#track` potrebbe essere simile a:

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
