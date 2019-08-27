---
seo-title: Debugging SDK
title: Debugging SDK
uuid: a 5972 d 87-c 593-4 b 4 f-a 56 f-dca 6 e 25268 e 1
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# Debugging SDK{#sdk-debugging}

Potete abilitare e disabilitare la registrazione. L'SDK di Media fornisce un meccanismo di registrazione/registrazione esteso per tutta la pila di tracciamento multimediale. Potete attivare o disattivare la registrazione impostando `debugLogging` il flag sull'oggetto Config.

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

La libreria adbmobile fornisce il debug di debug attraverso il `setDebugLogging` metodo. La registrazione di debug deve essere impostata per `false` tutte le app di produzione.

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

## Utilizzo di Adobe Bloodhound per testare le applicazioni Chromecast

Durante lo sviluppo dell'applicazione, Bloodhound consente di visualizzare le chiamate al server localmente e, facoltativamente, di inoltrare i dati ai server di raccolta Adobe. Per ulteriori informazioni su Bloodhound, consulta le guide seguenti:

* [Bloodhound 3.x per Mac](https://marketing.adobe.com/resources/help/en_US/mobile/bloodhound/)
* [Bloodhound 2.2 per Windows](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)

>[!IMPORTANT]
>
>Dal 30 aprile 2017, Adobe Bloodhound è stato ritirato. A partire dal 1° maggio 2017, non verranno più forniti ulteriori miglioramenti né supporto aggiuntivo Engineering o Adobe Expert Care.

## Messaggi registro

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

Per verificare l'implementazione, puoi utilizzare i file di registro della libreria Media SDK. Una strategia valida consiste nel cercare i registri per la stringa `#track`. Questo evidenzia tutte `track*()` le chiamate effettuate dall'applicazione.

Ad esempio, i file di registro per i quali `#track` sono stati filtrati possono essere:

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

