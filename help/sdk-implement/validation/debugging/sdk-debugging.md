---
seo-title: Debugging SDK
title: Debugging SDK
uuid: a 5972 d 87-c 593-4 b 4 f-a 56 f-dca 6 e 25268 e 1
translation-type: tm+mt
source-git-commit: 6b6caa59ac9ea14a42337e2f133ecb31f30491c7

---


# SDK debugging{#sdk-debugging}

Potete abilitare e disabilitare la registrazione. Media SDK offre un meccanismo di registrazione/di registrazione esteso che viene messo a disposizione nell'intero stack di tracciamento video. You can enable or disable this logging by setting the `debugLogging` flag on the Config object.

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

The ADBMobile library provides debug logging through the `setDebugLogging` method. Debug logging should be set to `false` for all the production apps.

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

**Utilizzo di Adobe Bloodhound per testare applicazioni Chromecast -**

Durante lo sviluppo dell'applicazione, Bloodhound consente di visualizzare le chiamate al server localmente e, facoltativamente, di inoltrare i dati ai server di raccolta Adobe. Per ulteriori informazioni su Bloodhound, consulta le guide seguenti:

* [Bloodhound 3.x per Mac](https://marketing.adobe.com/resources/help/en_US/mobile/bloodhound/)
* [Bloodhound 2.2 per Windows](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)

>[!IMPORTANT]
>
>Dal 30 aprile 2017, Adobe Bloodhound è stato ritirato. A partire dal 1° maggio 2017, non verranno più forniti ulteriori miglioramenti né supporto aggiuntivo Engineering o Adobe Expert Care.

### Messaggi registro

I messaggi di registro seguono questo formato:

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>] 
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **timestamp:** Questa è l'ora corrente della CPU (con data e ora per GMT)
* **livello:** Sono stati definiti 4 livelli di messaggio:
   * INFO - In genere i dati di input dell'applicazione (nome del lettore o ID video, ecc.)
   * DEBUG - Registri di debug, utilizzati dagli sviluppatori per eseguire il debug di problemi più complessi
   * AVVISO - Indica potenziali errori di integrazione/configurazione o bug Heartbeats SDK
   * ERROR - Indica errori di integrazione importanti o bug Heartbeats SDK
* **tag:** Nome del componente secondario che ha emesso il messaggio di registro (in genere il nome della classe)
* **message:** Il messaggio di trace effettivo

Puoi utilizzare i file di registro per la libreria heartbeat video per verificare l'implementazione. A good strategy is to search through the logs for the string `#track`. This will highlight all the `track*()` calls made by your application.

For instance, this is what the logs filtered for `#track` could look like:

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

