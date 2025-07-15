---
title: Spiegazione implementazione SDK per contenuti multimediali
description: Scopri come impostare Media SDK per il tracciamento dei contenuti multimediali nelle applicazioni mobili, OTT e browser (JS).
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
exl-id: a175332e-0bdc-44aa-82cb-b3f879e7abfc
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 94%

---

# Legacy - Panoramica della configurazione di Media SDK {#setup-overview}

Dopo aver scaricato Media SDK per la tua app video o il tuo lettore, segui le informazioni in questa sezione per configurare e implementare Media SDK.


## Linee guida generali sull’implementazione {#general-implementation-guidelines}

Esistono tre componenti principali di SDK utilizzati nel tracciamento con Streaming Media Collection:
* Configurazione Media Heartbeat - `MediaHeartbeatConfig` contiene le impostazioni di base per la generazione di rapporti.
* Delegato Media Heartbeat - `MediaHeartbeatDelegate` controlla il tempo di riproduzione e l’oggetto QoS.
* Media Heartbeat - `MediaHeartbeat` è la libreria principale contenente membri e metodi.

## Implementare Streaming Media SDK

Per configurare e utilizzare Streaming Media SDK, effettua i seguenti passaggi di implementazione:

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

   |  Nome metodo  |  Descrizione | Obbligatorio |
   | --- | --- | :---: |
   | `getQoSObject()` | Restituisce l&#39;istanza `MediaObject` che contiene le informazioni QoS correnti. Questo metodo verrà chiamato più volte durante una sessione di riproduzione. L&#39;implementazione del lettore deve restituire sempre i dati QoS disponibili più di recente. | Sì |
   | `getCurrentPlaybackTime()` | Restituisce la posizione corrente dela testina di riproduzione. <br /> Per il tracciamento VOD, il valore è specificato in secondi dall&#39;inizio dell&#39;elemento multimediale. <br /> Per lo streaming live, se il lettore non fornisce informazioni sulla durata del contenuto, il valore può essere specificato come il numero di secondi trascorsi dalla mezzanotte UTC di quel giorno. <br /> Nota: quando si utilizzano gli indicatori di avanzamento, è necessario specificare la durata del contenuto e la testina di riproduzione deve essere aggiornata come numero di secondi dall’inizio dell’elemento multimediale, a partire da 0. | Sì |

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
