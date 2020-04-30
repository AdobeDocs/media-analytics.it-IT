---
title: Configurazione iOS
description: Configurazione dell’applicazione Media SDK per l’implementazione su iOS.
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# Configurazione iOS{#set-up-ios}

## Prerequisiti

* **Ottenete parametri di configurazione validi per Media SDK** Questi parametri possono essere ottenuti da un rappresentante Adobe dopo la configurazione dell&#39;account di analisi.
* **Implementa ADBMobile per iOS nella tua applicazione** Per ulteriori informazioni sulla documentazione SDK per Adobe Mobile, consulta SDK 4.x per [iOS per le soluzioni Experience Cloud.](https://docs.adobe.com/content/help/it-IT/mobile-services/ios/overview.html)

   >[!IMPORTANT]
   >
   >A partire da iOS 9, Apple ha introdotto una funzione denominata App Transport Security (ATS). Questa funzione mira a migliorare la sicurezza della rete assicurandosi che le app utilizzino solo protocolli e cifratori standard di settore. Questa funzione è abilitata per impostazione predefinita, ma sono disponibili opzioni di configurazione che consentono di utilizzare ATS. Per informazioni dettagliate su ATS, consultate [App Transport Security (Protezione trasporto app).](https://docs.adobe.com/content/help/en/mobile-services/ios/config-ios/app-transport-security.html)

* **Fornite le seguenti funzionalità nel lettore multimediale:**

   * _Un&#39;API per iscriversi agli eventi_ del lettore - L&#39;SDK di Media richiede che venga chiamato un set di API semplici quando si verificano eventi nel lettore.
   * _API che fornisce informazioni_ sul lettore - Queste informazioni includono dettagli quali il nome del supporto e la posizione della testina di riproduzione.

## Implementazione SDK

1. Aggiungi l’SDK per file multimediali [scaricato](/help/sdk-implement/download-sdks.md#download-2x-sdks) al progetto.

   1. Verificate che nella `libs` directory siano presenti i seguenti componenti software:

      * `ADBMediaHeartbeat.h`: Il file di intestazione Objective-C utilizzato per le API di tracciamento heartbeat iOS.
      * `ADBMediaHeartbeatConfig.h`: Il file di intestazione Objective-C per la configurazione dell&#39;SDK.
      * `MediaSDK.a`: fat binary abilitato per bitcode contenente le build della libreria per dispositivi (armv7, armv7s, arm64) e simulatori (i386 e x86_64) iOS.

         Se la destinazione sarà un&#39;app iOS, il binary deve essere collegato.

      * `MediaSDK_TV.a`: Un fat binary abilitato per bitcode contenente le build della libreria per i nuovi dispositivi Apple TV (arm64) e simulatori (x86_64).

         Il binario deve essere collegato quando la destinazione è destinata a un&#39;app Apple TV (tvOS).
   1. Aggiungi la libreria al progetto:

      1. Avvia l&#39;IDE di Xcode e apri la tua app.
      1. In **[!UICONTROL Project Navigator]**, trascinate la `libs` directory e rilasciatela sotto il progetto.

      1. Assicurarsi che la **[!UICONTROL Copy Items if Needed]** casella di controllo sia selezionata, che **[!UICONTROL Create Groups]** sia selezionata e che nessuna delle caselle di controllo in **[!UICONTROL Add to Target]** sia selezionata.

         ![](assets/choose-options_ios.png)

      1. Fai clic su **[!UICONTROL Finish]**.
      1. In **[!UICONTROL Project Navigator]**, selezionate l&#39;app e le destinazioni.
      1. Link the required frameworks and libraries in the **[!UICONTROL Linked Frameworks]** and **[!UICONTROL Libraries]** section on the **[!UICONTROL General]** tab.

         **Destinazioni di app iOS:**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**
         **Destinazioni Apple TV (tvOS):**

         * **AdobeMobileLibrary_TV.a**
         * **MediaSDK_TV.a**
         * **libsqlite3.0.tbd**
         * **SystemConfiguration.framework**
      1. Verificate che l&#39;app venga generata senza errori.




1. Importa la libreria.

   ```
   #import "ADBMediaHeartbeat.h" 
   #import "ADBMediaHeartbeatConfig.h" 
   ```

1. Create un&#39; `ADBMediaHeartbeatConfig` istanza.

   Questa sezione spiega come comprendere i parametri di `MediaHeartbeat` configurazione e impostare i valori di configurazione corretti nell’istanza per un `MediaHeartbeat` monitoraggio accurato.

   Esempio di inizializzazione `ADBMediaHeartbeatConfig`:

   ```
   // Media Heartbeat Initialization 
   ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
   config.trackingServer = <SAMPLE_HEARTBEAT_TRACKING_SERVER>; 
   config.channel        = <SAMPLE_HEARTBEAT_CHANNEL>; 
   config.appVersion     = <SAMPLE_HEARTBEAT_SDK_VERSION>; 
   config.ovp            = <SAMPLE_HEARTBEAT_OVP_NAME>; 
   config.playerName     = <SAMPLE_PLAYER_NAME>; 
   config.ssl            = <YES/NO>; 
   config.debugLogging   = <YES/NO>; 
   ```

1. Implementa il `ADBMediaHeartbeatDelegate` protocollo.

   ```
   @interface VideoAnalyticsProvider : NSObject <ADBMediaHeartbeatDelegate> 
   
   @end 
   
   @implementation VideoAnalyticsProvider 
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames>  
   // with the current playback QoS values. 
   - (ADBMediaObject *)getQoSObject { 
       return [ADBMediaHeartbeat createQoSObjectWithBitrate:<bitrate>  
                                 startupTime:<startuptime>   
                                 fps:<fps>  
                                 droppedFrames:<droppedFrames>]; 
   } 
   
   // Return the current video player playhead position. 
   // Replace <currentPlaybackTime> with the video player current playback time 
   - (NSTimeInterval)getCurrentPlaybackTime { 
       return <currentPlaybackTime>; 
   } 
   
   @end
   ```

1. Utilizzate l&#39;icona `ADBMediaHeartBeatConfig` e `ADBMediaHeartBeatDelegate` per creare l&#39; `ADBMediaHeartbeat` istanza.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance 
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate: 
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Accertatevi che l’ `ADBMediaHeartbeat` istanza sia accessibile e che *non venga deallocata fino alla fine della sessione*. Questa istanza verrà utilizzata per tutti i seguenti eventi di tracciamento.

## Migrazione dalla versione 1.x alla 2.x in iOS {#migrate-to-two-x}

Nella versione 2.x, tutti i metodi pubblici sono consolidati nella `ADBMediaHeartbeat` classe per semplificare gli sviluppatori. Tutte le configurazioni sono state consolidate nella `ADBMediaHeartbeatConfig` classe.

Per ulteriori informazioni sulla migrazione da 1.x a 2.x, consulta Migrazione [VHL 1.x a 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## Configurare un&#39;app nativa per tvOS

Con il rilascio della nuova Apple TV, ora è possibile creare applicazioni da eseguire nell&#39;ambiente tvOS nativo. Potete creare un&#39;app puramente nativa, utilizzando diversi framework disponibili in iOS, oppure potete creare l&#39;app utilizzando modelli XML e JavaScript. A partire da MediaSDK versione 2.0, è disponibile il supporto per tvOS. Per ulteriori informazioni su tvOS, vedi [tvOS Developer site.](https://developer.apple.com/tvos/)

Effettuare le seguenti operazioni nel progetto Xcode. Questa guida viene scritta partendo dal presupposto che il progetto abbia una destinazione che sia un&#39;app Apple TV per tvOS:

1. Trascinate il file della `VideoHeartbeat_TV.a` libreria nella `lib` cartella del progetto.

1. In the **[!UICONTROL Build Phases]** tab of your tvOS app’s target, expand the **[!UICONTROL Link Binary with Libraries]** section and add the following libraries:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`

