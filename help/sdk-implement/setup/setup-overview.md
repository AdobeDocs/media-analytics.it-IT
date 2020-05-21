---
title: Panoramica configurazione
description: Panoramica dell’impostazione di Media SDK per il tracciamento dei contenuti multimediali nelle applicazioni mobili, OTT e browser (JS).
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
translation-type: tm+mt
source-git-commit: 300eb77858296f0246a2cb484386c0dcdf8b87b9
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 14%

---


# Panoramica configurazione{#setup-overview}

>[!IMPORTANT]
>
>Con la fine del supporto per gli SDK della versione 4 per dispositivi mobili il 31 agosto 2021, Adobe interromperà anche il supporto per gli SDK di Media Analytics per iOS e Android.  Per ulteriori informazioni, consultate Domande frequenti relative alla fine del supporto per l’SDK di [Media Analytics](/help/sdk-implement/end-of-support-faqs.md).

Le seguenti istruzioni sono valide per gli SDK Media 2.x. Se stai implementando una versione 1.x dell’SDK per file multimediali, consulta la Documentazione dell’SDK per file multimediali [1.x.](/help/sdk-implement/download-sdks.md) Per gli integratori Primetime, consulta la documentazione _SDK per_ Primetime Media.

## Supporto versione minima della piattaforma {#minimum-platform-version}

La tabella seguente riassume le versioni minime delle piattaforme supportate per ogni SDK, iniziando il 19 febbraio 2019.

| Sistema operativo/browser | Versione minima richiesta |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0+ - Lollipop |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## Linee guida generali per l’implementazione {#general-implementation-guidelines}

Il tracciamento dei contenuti multimediali è composto da tre componenti SDK principali:
* Configurazione Media Heartbeat - La configurazione contiene le impostazioni di base per il reporting.
* Delegato Heartbeat Media - Il delegato controlla il tempo di riproduzione e l&#39;oggetto QoS.
* Media Heartbeat - La libreria principale contenente membri e metodi.

Completa i seguenti passaggi di implementazione:

1. Create un&#39; `MediaHeartbeatConfig` istanza e impostate i valori dei parametri di configurazione.

   |  Nome della variabile  | Descrizione  | Obbligatorio |  Valore predefinito  |
   |---|---|:---:|---|
   | `trackingServer` | Server di tracciamento per l&#39;analisi dei supporti. Questa funzione è diversa dal server di tracciamento analisi. | Sì | Stringa vuota |
   | `channel` | Nome del canale | No | Stringa vuota |
   | `ovp` | Nome della piattaforma multimediale online tramite la quale viene distribuito il contenuto | No | Stringa vuota |
   | `appVersion` | Versione dell’app lettore multimediale/SDK | No | Stringa vuota |
   | `playerName` | Nome del lettore multimediale in uso, ad esempio &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom Player&quot; | No | Stringa vuota |
   | `ssl` | Indica se le chiamate devono essere effettuate tramite HTTPS | No | false |
   | `debugLogging` | Indica se la registrazione di debug è abilitata | No | false |

1. Implementare `MediaHeartbeatDelegate`.

   |  Nome metodo  |  Descrizione  | Obbligatorio |
   | --- | --- | :---: |
   | `getQoSObject()` | Restituisce l&#39;istanza `MediaObject` che contiene le informazioni QoS correnti. Questo metodo verrà chiamato più volte durante una sessione di riproduzione. L&#39;implementazione del lettore deve restituire sempre i dati QoS disponibili più di recente. | Sì |
   | `getCurrentPlaybackTime()` | Restituisce la posizione corrente dell&#39;indicatore di riproduzione. Per il tracciamento VOD, il valore è specificato in secondi dall&#39;inizio dell&#39;elemento multimediale. Per il tracciamento LINEAR/LIVE, il valore è specificato in secondi dall&#39;inizio del programma. | Sì |

   >[!TIP]
   >
   >L&#39;oggetto Quality of Service (QoS) è facoltativo. Se i dati QoS sono disponibili per il lettore e si desidera tenerne traccia, sono necessarie le seguenti variabili:

   | Nome della variabile | Descrizione   | Obbligatorio |
   | --- | --- | :---: |
   | `bitrate` | Bitrate del supporto in bit al secondo. | Sì |
   | `startupTime` | Tempo di avvio del supporto, in millisecondi. | Sì |
   | `fps` | I fotogrammi visualizzati al secondo. | Sì |
   | `droppedFrames` | Numero di fotogrammi saltati finora. | Sì |

1. Create l’ `MediaHeartbeat` istanza.

   Utilizzate l&#39;icona `MediaHertbeatConfig` e `MediaHertbeatDelegate` per creare l&#39; `MediaHeartbeat` istanza.

   >[!IMPORTANT]
   >
   >Accertatevi che l’ `MediaHeartbeat` istanza sia accessibile e non venga deallocata fino alla fine della sessione. Questa istanza verrà utilizzata per tutti i seguenti eventi di tracciamento dei supporti.

   >[!TIP]
   >
   >`MediaHeartbeat` richiede un&#39;istanza di `AppMeasurement` invio di chiamate ad Adobe Analytics.

1. Combinate tutti i pezzi.

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

* Le chiamate per contenuti multimediali e ad Start vengono inviate direttamente al server Adobe Analytics (AppMeasurement).
* Le chiamate Heartbeat vengono inviate al server di tracciamento di Media Analytics (heartbeat), elaborate e trasmesse al server Adobe Analytics.

* **Server** Adobe Analytics (AppMeasurement) Per ulteriori informazioni sulle opzioni del server di tracciamento, vedi Compilazione [corretta delle variabili trackingServer e trackingServerSecure.](https://helpx.adobe.com/it/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >Per il servizio ID visitatore Experience Cloud è necessario un server di tracciamento RDC o una risoluzione CNAME per un server RDC.

   Il server di tracciamento analisi deve terminare in &quot;`.sc.omtrdc.net`&quot; o essere un CNAME.

* ** Server Media Analytics (Heartbeats)**Questo ha sempre il formato &quot;`[your_namespace].hb.omtrdc.net`&quot;. Il valore &quot;`[your_namespace]`&quot; specifica la società e viene fornito da Adobe.

Il tracciamento dei file multimediali funziona allo stesso modo su tutte le piattaforme, desktop e dispositivi mobili. Il tracciamento audio funziona attualmente sulle piattaforme mobili. Per tutte le chiamate di tracciamento, sono disponibili alcune variabili universali chiave da convalidare:

## Documentazione SDK 1.x {#sdk-1x-documentation}

| SDK 1.x di Video Analytics  |  Guide per sviluppatori (solo PDF) |
| --- | --- |
| Android | [Configura per Android ](vhl-dev-guide-v15_android.pdf) |
| AppleTV | [Configurare per AppleTV ](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Configura per Chromecast ](chromecast_1.x_sdk.pdf) |
| iOS | [Configurare per iOS ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [Configurare per JavaScript ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android:   [Configurare Media Analytics](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS:   [Configurare Media Analytics](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS:   [Configurare Media Analytics](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [Configurare per TVML ](vhl_tvml.pdf) |

## Documentazione Primetime Media SDK {#primetime-docs}

* [Guide utente Primetime](https://helpx.adobe.com/it/primetime/user-guide.html)
