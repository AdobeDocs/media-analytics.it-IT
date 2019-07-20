---
seo-title: Panoramica della configurazione
title: Panoramica della configurazione
uuid: 06 fefedb-b 0 c 8-4 f 7 d -90 c 8-e 374 cdde 1695
translation-type: tm+mt
source-git-commit: 63fb6332694675cd03843995f8f86ae45973d399

---


# Setup Overview{#setup-overview}

>[!IMPORTANT]
>
>Le istruzioni seguenti sono valide per gli SDK 2. x multimediali. If you are implementing a 1.x version of the Media SDK, see the [1.x Media SDK Documentation.](../download-sdks.md) Per gli integratori Primetime, vedi _la documentazione Primetime Media SDK_ di seguito.


## Minimum Platform Version Support {#minimum-platform-version}

La tabella seguente descrive le versioni minime della piattaforma supportate per ciascun SDK, a partire dal 19 febbraio 2019.

| OS/Browser | Versione min. |
| --- | --- |
| iOS  | iOS  6+ |
| Android | Android 5.0 + - Lollipop |
| Chrome | v 22 + |
| Mozilla | v 27 + |
| Safari | v 7 + |
| IE | v 11 + |

## General Implementation Guidelines {#section_965A3B699A8248DDB9B2B3EA3CC20E41}

Il tracciamento multimediale include tre componenti SDK principali:
* Configurazione Media Heartbeat - La configurazione contiene le impostazioni di base per il reporting.
* Media Heartbeat Delegate - Il valore delegate controlla il tempo di riproduzione e l'oggetto qos.
* Media Heartbeat - La libreria principale contenente membri e metodi.

Completa i seguenti passaggi di implementazione:

1. Create a `MediaHeartbeatConfig` instance and set your config parameter values.

   |  Nome della variabile  | Descrizione  | Obbligatorio |  Valore predefinito  |
   |---|---|:---:|---|
   | `trackingServer` | Server di tracciamento per analisi file multimediali. Questo è diverso dal server di tracciamento analisi. | Sì | Stringa vuota |
   | `channel` | Nome del canale | No | Stringa vuota |
   | `ovp` | Nome della piattaforma multimediale online attraverso il quale viene distribuito il contenuto | No | Stringa vuota |
   | `appVersion` | Versione dell'app o dell'SDK per il lettore multimediale | No | Stringa vuota |
   | `playerName` | Nome del lettore multimediale in uso, ovvero "avplayer", "HTML 5 Player", "Lettore personalizzato" | No | Stringa vuota |
   | `ssl` | Indica se le chiamate devono essere effettuate mediante HTTPS | No | false |
   | `debugLogging` | Indica se la registrazione di debug è abilitata | No | false |

1. Implement the `MediaHeartbeatDelegate`.

   | Nome metodo  |  Descrizione  | Obbligatorio |
   | --- | --- | :---: |
   | `getQoSObject()` | Returns the `MediaObject` instance that contains the current QoS information. Questo metodo verrà chiamato più volte durante una sessione di riproduzione. L'implementazione del lettore deve restituire sempre i dati qos disponibili più di recente. | Sì |
   | `getCurrentPlaybackTime()` | Restituisce la posizione corrente dell'indicatore di riproduzione. Per il tracciamento VOD, il valore è specificato in secondi dall'inizio dell'elemento multimediale. Per il monitoraggio LINEARE/LIVE, il valore viene specificato in secondi dall'inizio del programma. | Sì |

   >[!TIP]
   >
   >L'oggetto Quality of Service (qos) è facoltativo. Se sono disponibili dati qos per il lettore e desideri tenere traccia di tali dati, sono necessarie le seguenti variabili:

   | Nome variabile | Descrizione   | Obbligatorio |
   | --- | --- | :---: |
   | `bitrate` | Bitrate di elementi multimediali in bit al secondo. | Sì |
   | `startupTime` | L'ora di inizio dei contenuti multimediali, in millisecondi. | Sì |
   | `fps` | Fotogrammi visualizzati al secondo. | Sì |
   | `droppedFrames` | Numero di fotogrammi rilasciati finora. | Sì |

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHertbeatConfig` and `MediaHertbeatDelegate` to create the `MediaHeartbeat` instance.

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the session. Questa istanza verrà utilizzata per tutti i seguenti eventi di tracciamento multimediali.

   >[!TIP]
   >
   >`MediaHeartbeat` richiede un'istanza di `AppMeasurement` invio di chiamate ad Adobe Analytics.

1. Combinate tutti i pezzi.

   Il seguente codice di esempio utilizza il nostro SDK javascript 2. x per un lettore video HTML 5:

   ```javascript
   // Create local references to the heartbeat classes 
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   
   //Media Heartbeat Config 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = "namespace.hb.omtrdc.net"; 
   mediaConfig.playerName = "HTML5 Basic"; 
   mediaConfig.channel = "Video Channel"; 
   mediaConfig.debugLogging = true; 
   mediaConfig.appVersion = "2.0"; 
   mediaConfig.ssl = false; 
   mediaConfig.ovp = ""; 
   
   // Media Heartbeat Delegate 
   var mediaDelegate = new MediaHeartbeatDelegate(); 
   
   // Set mediaDelegate CurrentPlaybackTime 
   mediaDelegate.getCurrentPlaybackTime = function() { 
       return video.currentTime; 
   }; 
   
   // Set mediaDelegate QoSObject - OPTIONAL 
   mediaDelegate.getQoSObject = function() { 
       return MediaHeartbeat.createQoSObject(video.bitrate,  
                                             video.startuptime,  
                                             video.fps,  
                                             video.droppedframes); 
   } 
   // Create mediaHeartbeat instance      
   this.mediaHeartbeat =  
     new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurementInstance);  
   ```

## Validate {#section_D4D46F537A4E442B8AB0BB979DDAA4CC}

Le implementazioni multimediali sono costituite da due tipi di chiamate di tracciamento:

* Le chiamate a supporti e avvio annunci vengono inviate direttamente al server appmeasurement.
* Le chiamate Heartbeat vengono inviate al server di tracciamento Heartbeat all'avvio, ogni dieci secondi per il contenuto e ogni secondo per annunci pubblicitari.

Il monitoraggio dei contenuti multimediali funziona allo stesso modo su tutte le piattaforme, desktop e dispositivi mobili. Il tracciamento audio attualmente funziona sulle piattaforme mobili. Per tutte le chiamate di tracciamento è possibile convalidare alcune variabili universali chiave:

* **Appmeasurement (Analytics)**
Per ulteriori informazioni sulle opzioni del server di tracciamento, vedi [Compilazione corretta delle variabili trackingserver e trackingserversecure.](https://marketing.adobe.com/resources/help/kb/en_US/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >Per il servizio ID visitatore di Experience Cloud è necessario un server di tracciamento RDC o CNAME che risolve un server RDC.

   The analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

* **Heartbeats (Media Analytics)**
È sempre dotato del formato "`[namespace].hb.omtrdc.net`, dove"`[namespace]`è definito dalla società di accesso e fornito da Adobe.

## SDK 1.x Documentation {#section_acj_tkk_t2b}

| SDK di Video Analytics 1. x  | Guide per sviluppatori (solo PDF) |
| --- | --- |
| Android | [Configurazione per Android ](vhl-dev-guide-v15_android.pdf) |
| AppleTV | [Configura per appletv ](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Configura per Chromecast ](chromecast_1.x_sdk.pdf) |
| App | [Configurazione per iOS ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [Configurare per javascript ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [Configurare per TVML ](vhl_tvml.pdf) |

## Primetime Media SDK Documentation {#primetime-docs}

* [Guide utente Primetime](https://helpx.adobe.com/primetime/user-guide.html)