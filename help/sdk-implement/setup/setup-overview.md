---
title: Spiegazione implementazione SDK per contenuti multimediali
description: “Scopri come configurare Media SDK per il tracciamento dei contenuti multimediali nelle applicazioni mobili, OTT e browser (JS)”.
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
exl-id: a175332e-0bdc-44aa-82cb-b3f879e7abfc
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 165c7f01a2d2c32df518c89a5c49637107d41086
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 92%

---

# Panoramica dell’installazione {#setup-overview}

Le seguenti istruzioni sono valide per gli SDK di contenuti multimediali 2.x. Se implementi una versione 1.x dell’SDK di contenuti multimediali, consulta la [Documentazione 1.x Media SDK.](/help/sdk-implement/download-sdks.md) Per gli integratori Primetime, vedi _Documentazione di Primetime Media SDK_ sotto.

>[!IMPORTANT]
>
>Con la fine del supporto per gli SDK per dispositivi mobili versione 4, il 31 agosto 2021, Adobe terminerà anche il supporto per gli SDK Media Analytics per iOS e Android.  Per ulteriori informazioni, consulta [Domande frequenti sull’SDK di Media Analytics relative alla fine del supporto](/help/sdk-implement/end-of-support-faqs.md).


## Supporto versione minima della piattaforma {#minimum-platform-version}

La tabella seguente descrive le versioni minime della piattaforma supportate per ogni SDK, a partire dal 19 febbraio 2019.

| Sistema operativo/browser | Versione minima richiesta |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0+ - Lollipop |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## Linee guida generali sull’implementazione {#general-implementation-guidelines}

Il tracciamento dei contenuti multimediali è costituito da tre componenti SDK principali:
* Configurazione Media Heartbeat - La configurazione contiene le impostazioni di base per il reporting.
* Delegato Media Heartbeat - Il delegato controlla il tempo di riproduzione e l’oggetto QoS.
* Media Heartbeat - La libreria principale contenente membri e metodi.

Completa i seguenti passaggi per l’implementazione:

1. Crea un’istanza `MediaHeartbeatConfig` e imposta i valori dei parametri di configurazione.

   |  Nome variabile  | Descrizione  | Obbligatorio |  Valore predefinito  |
   |---|---|:---:|---|
   | `trackingServer` | Server di tracciamento per l’analisi dei contenuti multimediali. Questa funzione è diversa dal server di tracciamento di Analytics. | Sì | Stringa vuota |
   | `channel` | Nome del canale | No | Stringa vuota |
   | `ovp` | Nome della piattaforma multimediale online attraverso la quale il contenuto è distribuito | No | Stringa vuota |
   | `appVersion` | Versione dell’app/SDK del lettore multimediale | No | Stringa vuota |
   | `playerName` | Nome del lettore multimediale in uso (ad esempio “AVPlayer”, “HTML5 Player”, “My Custom Player”) | No | Stringa vuota |
   | `ssl` | Indica se le chiamate devono essere effettuate tramite HTTPS | No | false |
   | `debugLogging` | Indica se la registrazione di debug è abilitata | No | false |

1. Implementa `MediaHeartbeatDelegate`.

   |  Nome metodo  |  Descrizione  | Obbligatorio |
   | --- | --- | :---: |
   | `getQoSObject()` | Restituisce l&#39;istanza `MediaObject` che contiene le informazioni QoS correnti. Questo metodo verrà chiamato più volte durante una sessione di riproduzione. L&#39;implementazione del lettore deve restituire sempre i dati QoS disponibili più di recente. | Sì |
   | `getCurrentPlaybackTime()` | Restituisce la posizione corrente dell&#39;indicatore di riproduzione. <br /> Per il tracciamento VOD, il valore è specificato in secondi dall&#39;inizio dell&#39;elemento multimediale. <br /> Per lo streaming live, se il lettore non fornisce informazioni sulla durata del contenuto, il valore può essere specificato come numero di secondi dalla mezzanotte UTC di quel giorno. <br /> Nota: Quando si utilizzano i marcatori di avanzamento, è necessaria la durata del contenuto e l’indicatore di riproduzione deve essere aggiornato come numero di secondi dall’inizio dell’elemento multimediale, a partire da 0. | Sì |

   >[!TIP]
   >
   >L’oggetto Quality of Service (QoS) è facoltativo. Se i dati QoS sono disponibili per il lettore e desideri tenere traccia di tali dati, sono necessarie le seguenti variabili:

   | Nome variabile | Descrizione   | Obbligatorio |
   | --- | --- | :---: |
   | `bitrate` | Il bitrate del supporto in bit al secondo. | Sì |
   | `startupTime` | Tempo di avvio del contenuto multimediale in millisecondi. | Sì |
   | `fps` | I fotogrammi visualizzati al secondo. | Sì |
   | `droppedFrames` | Numero di fotogrammi saltati finora. | Sì |

1. Crea l’istanza `MediaHeartbeat`.

   Utilizza `MediaHertbeatConfig` e `MediaHertbeatDelegate` per creare l’istanza `MediaHeartbeat`.

   >[!IMPORTANT]
   >
   >Assicurati che l’istanza `MediaHeartbeat` sia accessibile e non venga deassegnata fino alla fine della sessione. Questa istanza verrà utilizzata per tutti i seguenti eventi di tracciamento multimediale.

   >[!TIP]
   >
   >`MediaHeartbeat` richiede un’istanza di `AppMeasurement` per inviare chiamate ad Adobe Analytics.

1. Combina tutti i pezzi.

   Il seguente codice di esempio utilizza l’SDK JavaScript 2.x per un lettore video HTML5:

   ```javascript
   // Create local references to the heartbeat classes
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   
   //Media Heartbeat Config
   var mediaConfig = new MediaHeartbeatConfig();
   mediaConfig.trackingServer = "[your_namespace].hb.omtrdc.net";
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

## Convalida {#validate}

Le implementazioni di tracciamento di Media Analytics generano due tipi di chiamate di tracciamento:

* Le chiamate Media e Ad Start vengono inviate direttamente al server Adobe Analytics (AppMeasurement).
* Le chiamate Heartbeat vengono inviate al server di tracciamento di Media Analytics (heartbeat), vengono elaborate e trasmesse al server Adobe Analytics.

* **Server Adobe Analytics (AppMeasurement)**
Per ulteriori informazioni sulle opzioni del server di tracciamento, vedi [Compilare correttamente le variabili trackingServer e trackingServerSecure.](https://helpx.adobe.com/it/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >Per il servizio ID visitatore di Experience Cloud è necessario un server di monitoraggio RDC o la risoluzione CNAME in un server RDC.

   Il server di tracciamento di Analytics deve terminare in “`.sc.omtrdc.net`” o essere un CNAME.

* ** Server Media Analytics (Heartbeat)** 
Questo ha sempre il formato “`[your_namespace].hb.omtrdc.net`”. Il valore di “`[your_namespace]`” specifica la società ed è fornito da Adobe.

Il tracciamento dei contenuti multimediali funziona allo stesso modo su tutte le piattaforme, desktop e dispositivi mobili. Il tracciamento audio funziona attualmente sulle piattaforme mobili. Per tutte le chiamate di tracciamento sono disponibili alcune variabili universali chiave da convalidare:

## Documentazione di SDK 1.x {#sdk-1x-documentation}

| SDK per Video Analytics 1.x  |  Guide per sviluppatori (solo PDF) |
| --- | --- |
| Android | [Configurazione per Android ](vhl-dev-guide-v15_android.pdf) |
| AppleTV | [Configurazione per AppleTV ](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Configurazione per Chromecast ](chromecast_1.x_sdk.pdf) |
| iOS | [Configurazione per iOS ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [Configurazione per JavaScript ](vhl-dev-guide-v15_js.pdf) |
| Primetime  | <ul> <li> Android:   [Configurare Media Analytics](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS:   [Configurare Media Analytics](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS:   [Configurare Media Analytics](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [Configurazione per TVML ](vhl_tvml.pdf) |

## Documentazione di Primetime Media SDK {#primetime-docs}

* [Guide utente di Primetime](https://helpx.adobe.com/it/primetime/user-guide.html)
