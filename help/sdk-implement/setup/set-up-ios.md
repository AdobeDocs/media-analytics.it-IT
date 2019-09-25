---
seo-title: Configurare iOS
title: Configurare iOS
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Configurare iOS{#set-up-ios}

## Prerequisiti

* **Obtain valid configuration parameters for the Media SDK**
These parameters can be obtained from an Adobe representative after you set up your analytics account.
* **Implementa ADBMobile per iOS nella tua applicazione** Per ulteriori informazioni sulla documentazione SDK per Adobe Mobile, consulta SDK 4.x per [iOS per le soluzioni Experience Cloud.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/)

   >[!IMPORTANT]
   >
   >A partire da iOS 9, Apple ha introdotto una funzione denominata App Transport Security (ATS). Questa funzione mira a migliorare la sicurezza della rete assicurandosi che le app utilizzino solo protocolli e cifratori standard di settore. Questa funzione è abilitata per impostazione predefinita, ma sono disponibili opzioni di configurazione che consentono di utilizzare ATS. Per informazioni dettagliate su ATS, consultate [App Transport Security.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/app_transport_security.html)

* **Fornite le seguenti funzionalità nel lettore multimediale:**

   * _Un'API per iscriversi agli eventi_ del lettore - L'SDK di Media richiede che venga chiamato un set di API semplici quando si verificano eventi nel lettore.
   * _An API that provides player information - This information includes details such as the media name and the play head position._

## Implementazione SDK

1. Aggiungi l’SDK per file multimediali [scaricato](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) al progetto.

   1. Verificate che nella `libs` directory siano presenti i seguenti componenti software:

      * `ADBMediaHeartbeat.h`: Il file di intestazione Objective-C utilizzato per le API di tracciamento heartbeat iOS.
      * `ADBMediaHeartbeatConfig.h`: Il file di intestazione Objective-C per la configurazione SDK.
      * `MediaSDK.a`: fat binary abilitato per bitcode contenente le build della libreria per dispositivi (armv7, armv7s, arm64) e simulatori (i386 e x86_64) iOS.

         Se la destinazione sarà un'app iOS, il binary deve essere collegato.

      * `MediaSDK_TV.a`: Un fat binary abilitato per bitcode contenente le build della libreria per dispositivi (arm64) e simulatori (x86_64) Apple TV.

         Il binario deve essere collegato quando la destinazione è destinata a un'app Apple TV (tvOS).
   1. Aggiungi la libreria al progetto:

      1. Avvia l'IDE di Xcode e apri la tua app.
      1. In , drag the  directory and drop it under your project.**[!UICONTROL Project Navigator]**`libs`

      1. Ensure that the  checkbox is selected, the  is selected, and none of the checkboxes in  are selected.**[!UICONTROL Copy Items if Needed]****[!UICONTROL Create Groups]****[!UICONTROL Add to Target]**

         ![](assets/choose-options_ios.png)

      1. Fai clic su **[!UICONTROL Finish]**.
      1. In , select your app and select your targets.**[!UICONTROL Project Navigator]**
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
      1. Verificate che l'app venga generata senza errori.




1. Importa la libreria.

   ```
   #import "ADBMediaHeartbeat.h" 
   #import "ADBMediaHeartbeatConfig.h" 
   ```

1. Create a  instance.`ADBMediaHeartbeatConfig`

   This section helps you to understand the  config parameters, and to set correct config values on your  instance for accurate tracking.`MediaHeartbeat``MediaHeartbeat`

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

1. Implement the  protocol.`ADBMediaHeartbeatDelegate`

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

1. Use the  and  to create the  instance.`ADBMediaHeartBeatConfig``ADBMediaHeartBeatDelegate``ADBMediaHeartbeat`

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance 
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate: 
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Make sure that your  instance is accessible and does not get deallocated until the end of the session. `ADBMediaHeartbeat`** Questa istanza verrà utilizzata per tutti i seguenti eventi di tracciamento.

## Migrazione dalla versione 1.x alla 2.x in iOS {#migrate-to-two-x}

In version 2.x, all of the public methods are consolidated into the  class to make it easier on developers. `ADBMediaHeartbeat` Tutte le configurazioni sono state consolidate nella `ADBMediaHeartbeatConfig` classe.

Per ulteriori informazioni sulla migrazione da 1.x a 2.x, consulta Migrazione [VHL 1.x a 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## Configurare un'app nativa per tvOS

Con il rilascio della nuova Apple TV, ora è possibile creare applicazioni da eseguire nell'ambiente tvOS nativo. Potete creare un'app puramente nativa, utilizzando diversi framework disponibili in iOS, oppure potete creare l'app utilizzando modelli XML e JavaScript. A partire da MediaSDK versione 2.0, è disponibile il supporto per tvOS. Per ulteriori informazioni su tvOS, vedi [tvOS Developer site.](https://developer.apple.com/tvos/documentation/)

Effettuare le seguenti operazioni nel progetto Xcode. Questa guida viene scritta partendo dal presupposto che il progetto abbia una destinazione che sia un'app Apple TV per tvOS:

1. Trascinate il file della `VideoHeartbeat_TV.a` libreria nella `lib` cartella del progetto.

1. In the **[!UICONTROL Build Phases]** tab of your tvOS app’s target, expand the **[!UICONTROL Link Binary with Libraries]** section and add the following libraries:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`

