---
seo-title: Configurare iOS
title: Configurare iOS
uuid: a 1 c 6 be 79-a 6 dc -47 b 6-93 b 3-ac 7 b 42 f 1 f 3 eb
translation-type: tm+mt
source-git-commit: 63fb6332694675cd03843995f8f86ae45973d399

---


# Set up iOS{#set-up-ios}

## Prerequisiti

* **Ottenete parametri di configurazione validi per Media SDK**
Questi parametri possono essere ottenuti da un rappresentante Adobe dopo aver configurato il vostro account Analytics.
* **Implementazione di adbmobile per iOS nell'applicazione**
Per ulteriori informazioni sulla documentazione SDK di Adobe Mobile, consulta [SDK 4. x per iOS per le soluzioni Experience Cloud.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/)

   >[!IMPORTANT]
   >
   >A partire da iOS 9, Apple ha introdotto una funzionalità denominata App Transport Security (ATS). Questa funzione consente di migliorare la protezione della rete accertandosi che le app utilizzino solo protocolli e cifratori standard di settore. Questa funzione è abilitata per impostazione predefinita, ma hai opzioni di configurazione che offrono opzioni per l'utilizzo di ATS. For details on ATS, see [App Transport Security.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/app_transport_security.html)

* **Fornite le seguenti funzionalità nel lettore multimediale:**

   * _API per l'iscrizione agli eventi del lettore_ - L'SDK di Media richiede che venga chiamato un set di API semplici quando si verificano eventi nel lettore.
   * _API che fornisce informazioni_ sul lettore: informazioni dettagliate quali il nome del supporto e la posizione della testina di riproduzione.

## Implementazione SDK

1. Add your [downloaded](../../sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) Media SDK to your project.

   1. Verify that the following software components exist in the `libs` directory:

      * `ADBMediaHeartbeat.h`: Il file dell'intestazione Objective-C utilizzato per le API di tracciamento heartbeat iOS.
      * `ADBMediaHeartbeatConfig.h`: Il file dell'intestazione Objective-C per la configurazione SDK.
      * `MediaSDK.a`: Fat binary abilitato per bitcode contenente le build della libreria per dispositivi (armv 7, armv 7 s, arm 64) e simulatori (i 386 e x 86_ 64) iOS.

         Se la destinazione sarà un'app iOS, il binary deve essere collegato.

      * `MediaSDK_TV.a`: Fat binary abilitato per bitcode contenente le build della libreria per i nuovi dispositivi (arm 64) e simulatore (x 86_ 64) Apple TV.

         Questo binario deve essere collegato quando la destinazione è destinata a un'app Apple TV (tvos).
   1. Aggiungi la libreria al progetto:

      1. Avvia l'IDE di Xcode e apri la tua app.
      1. In **[!UICONTROL Project Navigator]**, drag the `libs` directory and drop it under your project.

      1. Ensure that the **[!UICONTROL Copy Items if Needed]** checkbox is selected, the **[!UICONTROL Create Groups]** is selected, and none of the checkboxes in **[!UICONTROL Add to Target]** are selected.

         ![](assets/choose-options_ios.png)

      1. Fai clic su **[!UICONTROL Finish]**.
      1. In **[!UICONTROL Project Navigator]**, select your app and select your targets.
      1. Link the required frameworks and libraries in the **[!UICONTROL Linked Frameworks]** and **[!UICONTROL Libraries]** section on the **[!UICONTROL General]** tab.

         **Destinazioni di app iOS:**

         * **AdobeMobileLibrary.a**
         * **Mediasdk. a**
         * **libsqlite3.0.tbd**
         **Destinazioni Apple TV (tvos):**

         * **AdobeMobileLibrary_TV.a**
         * **Mediasdk_ TV. a**
         * **libsqlite3.0.tbd**
         * **SystemConfiguration.framework**
      1. Verifica che l'app sia in grado di generare errori.




1. Importa la libreria.

   ```
   #import "ADBMediaHeartbeat.h" 
   #import "ADBMediaHeartbeatConfig.h" 
   ```

1. Create a `ADBMediaHeartbeatConfig` instance.

   This section helps you to understand the `MediaHeartbeat` config parameters, and to set correct config values on your `MediaHeartbeat` instance for accurate tracking.

   Esempio `ADBMediaHeartbeatConfig` di inizializzazione:

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

1. Implement the `ADBMediaHeartbeatDelegate` protocol.

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

1. Use the `ADBMediaHeartBeatConfig` and `ADBMediaHeartBeatDelegate` to create the `ADBMediaHeartbeat` instance.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance 
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate: 
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `ADBMediaHeartbeat` instance is accessible and *does not get deallocated until the end of the session*. Questa istanza verrà utilizzata per tutti i seguenti eventi di tracciamento.

## Migrating from version 1.x to 2.x in iOS {#migrate-to-two-x}

In version 2.x, all of the public methods are consolidated into the `ADBMediaHeartbeat` class to make it easier on developers. All configurations have been consolidated into the `ADBMediaHeartbeatConfig` class.

For more information about migrating from 1.x to 2.x, see [VHL 1.x to 2.x Migration.](../../sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## Configurare un'app nativa per tvos

Con il rilascio della nuova Apple TV, ora potete creare applicazioni da eseguire nell'ambiente nativo tvos. Puoi creare un'app puramente nativa, utilizzando uno qualsiasi di diversi framework disponibili in iOS, oppure puoi creare l'app utilizzando modelli XML e javascript. A partire dalla versione 2.0 di mediasdk, è disponibile il supporto per tvos. For more information about tvOS, see [tvOS Developer site.](https://developer.apple.com/tvos/documentation/)

Eseguite i seguenti passaggi nel progetto Xcode. Questa guida viene scritta presupponendo che il progetto abbia una destinazione di targeting delle app Apple TV tvos:

1. Drag the `VideoHeartbeat_TV.a` library file into your project’s `lib` folder.

1. In the **[!UICONTROL Build Phases]** tab of your tvOS app’s target, expand the **[!UICONTROL Link Binary with Libraries]** section and add the following libraries:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`

