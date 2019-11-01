---
title: Debug SDK
description: Questo argomento descrive il tracciamento e la registrazione disponibili in Media SDK.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Debug SDK{#sdk-debugging}

Potete attivare e disattivare la registrazione. L’SDK per file multimediali offre un ampio meccanismo di tracciamento/registrazione in tutto lo stack di tracciamento dei contenuti multimediali. È possibile abilitare o disabilitare la registrazione impostando il `debugLogging` flag sull'oggetto Config.

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

La libreria ADBMobile fornisce la registrazione di debug attraverso il `setDebugLogging` metodo. La registrazione di debug deve essere impostata su `false` per tutte le app di produzione.

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

## Utilizzo di Adobe Bloodhound per testare le applicazioni Chromecast

Durante lo sviluppo dell’applicazione, Bloodhound consente di visualizzare le chiamate server localmente e, facoltativamente, di inoltrare i dati ai server di raccolta Adobe. Per ulteriori informazioni su Bloodhound, consulta le guide seguenti:

* [Bloodhound 3.x per Mac](https://marketing.adobe.com/resources/help/en_US/mobile/bloodhound/)
* [Bloodhound 2.2 per Windows](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)

>[!IMPORTANT]
>
>Dal 30 aprile 2017, Adobe Bloodhound è stato
ritirato. A partire dal 1° maggio 2017, non verranno più forniti ulteriori miglioramenti né supporto aggiuntivo Engineering o Adobe Expert Care.

## Messaggi di registro

I messaggi di registro seguono questo formato:

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>] 
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **** timestamp: Ora CPU corrente (fuso orario per GMT)
* **** livello: Sono stati definiti 4 livelli di messaggio:
   * INFO - Solitamente i dati di input dell'applicazione (convalidate il nome del lettore, l'ID video, ecc.)
   * DEBUG - Registri di debug, utilizzati dagli sviluppatori per eseguire il debug di problemi più complessi
   * AVVERTENZA: indica potenziali errori di integrazione/configurazione o errori Heartbeat SDK
   * ERRORE - Indica importanti errori di integrazione o errori Heartbeat SDK
* **** tag: Nome del sottocomponente che ha emesso il messaggio di registro (in genere il nome della classe)
* **** message: Il messaggio di traccia effettivo

Puoi usare l’output dei file di registro dalla libreria Media SDK per verificare l’implementazione. Una buona strategia consiste nel cercare tra i file di registro la stringa `#track`. In questo modo verranno evidenziate tutte le `track*()` chiamate effettuate dall'applicazione.

Ad esempio, questo è l'aspetto dei file di registro filtrati per `#track` cui:

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

