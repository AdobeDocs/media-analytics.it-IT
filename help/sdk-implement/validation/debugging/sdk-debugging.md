---
title: Debug di SDK
description: Scopri le funzioni di tracciamento/registrazione disponibili in Media SDK.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
exl-id: c2de6454-8538-4d07-a099-e278b153d894
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 12%

---

# Debug dell’SDK{#sdk-debugging}

Puoi abilitare e disabilitare la registrazione. Media SDK fornisce un ampio meccanismo di tracciamento/registrazione in tutto lo stack di tracciamento dei contenuti multimediali. È possibile abilitare o disabilitare la registrazione impostando il flag `debugLogging` sull&#39;oggetto Config.

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

La libreria ADBMobile fornisce la registrazione di debug attraverso il metodo `setDebugLogging` . La registrazione di debug deve essere impostata su `false` per tutte le app di produzione.

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

## Utilizzo di Adobe Bloodhound per testare le applicazioni Chromecast

Durante lo sviluppo dell’applicazione, Bloodhound consente di visualizzare le chiamate server localmente e, facoltativamente, di inoltrare i dati ai server di raccolta Adobe.

<!--
For more information about Bloodhound, see the following guides:

* [Bloodhound 3.x for Mac](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=2ahUKEwiimfSUypDpAhVZHzQIHS6WDQIQFjABegQIChAD&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound%2F&usg=AOvVaw3t4s0gcvuWEpLIqBkhKdGH) 
* [Bloodhound 2.2 for Windows](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)
-->

>[!IMPORTANT]
>
>Dal 30 aprile 2017, Adobe Bloodhound è stato ritirato. A partire dal 1° maggio 2017, non verranno più forniti ulteriori miglioramenti né supporto aggiuntivo Engineering o Adobe Expert Care.

## Messaggi di registro

I messaggi di log seguono questo formato:

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>] 
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **timestamp:** è l’ora corrente della CPU (fuso orario per GMT)
* **livello:** sono definiti 4 livelli di messaggio:
   * INFO - Di solito i dati di input dall&#39;applicazione (convalidare il nome del lettore, l&#39;ID video, ecc.)
   * DEBUG - Log di debug, utilizzati dagli sviluppatori per eseguire il debug di problemi più complessi
   * AVVERTENZA: indica potenziali errori di integrazione/configurazione o bug dell&#39;SDK Heartbeat
   * ERRORE - Indica errori importanti di integrazione o bug dell&#39;SDK per Heartbeat
* **tag:** il nome del sottocomponente che ha emesso il messaggio di log (in genere il nome della classe)
* **messaggio:** messaggio di traccia effettivo

Puoi utilizzare l’output dei registri dalla libreria Media SDK per verificare l’implementazione. Una buona strategia è quella di cercare tra i log la stringa `#track`. In questo modo verranno evidenziate tutte le chiamate `track*()` effettuate dall&#39;applicazione.

Ad esempio, questo è l’aspetto dei log filtrati per `#track`:

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
