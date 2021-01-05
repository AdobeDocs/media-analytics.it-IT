---
title: Configurazione iOS
description: Configurazione dell’applicazione Media SDK per l’implementazione su iOS.
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
translation-type: tm+mt
source-git-commit: f54733c44e96c517d0c4c624a40742b421a54325
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 16%

---


# Configurazione iOS{#set-up-ios}

>[!IMPORTANT]
>
>Con la fine del supporto per gli SDK della versione 4 per dispositivi mobili il 31 agosto 2021,  Adobe interromperà anche il supporto per l’SDK di Media Analytics per iOS e Android.  Per ulteriori informazioni, consultate [Domande frequenti relative alla fine del supporto per l&#39;SDK di Media Analytics](/help/sdk-implement/end-of-support-faqs.md).

## Prerequisiti

* **Ottenete parametri di configurazione validi per Media**
SDKT: questi parametri possono essere ottenuti da un rappresentante di Adobe  una volta configurato l’account di analisi.
* **Implementa ADBMobile per iOS nell’**
applicazionePer ulteriori informazioni sulla documentazione dell’SDK per dispositivi mobili  Adobe, consulta SDK 4.x per  [iOS per le soluzioni  Experienci Cloud.](https://docs.adobe.com/content/help/it-IT/mobile-services/ios/overview.html)

   >[!IMPORTANT]
   >
   >A partire da iOS 9, Apple ha introdotto una funzione denominata App Transport Security (ATS). Questa funzione mira a migliorare la sicurezza della rete assicurandosi che le app utilizzino solo protocolli e cifratori standard di settore. Questa funzione è abilitata per impostazione predefinita, ma sono disponibili opzioni di configurazione che consentono di utilizzare ATS. Per informazioni dettagliate su ATS, vedere [App Transport Security (Protezione trasporto app).](https://docs.adobe.com/content/help/en/mobile-services/ios/config-ios/app-transport-security.html)

* **Fornite le seguenti funzionalità nel lettore multimediale:**

   * _Un&#39;API per iscriversi agli eventi_  del lettore. L&#39;SDK di Media richiede che venga chiamato un set di API semplici quando si verificano eventi nel lettore.
   * _API che fornisce informazioni_  sul lettore: queste informazioni includono dettagli quali il nome del supporto e la posizione della testina di riproduzione.

## Implementazione SDK

>[!IMPORTANT]
>
>A partire dalla versione 2.3.0, l’SDK viene distribuito tramite XCFrameworks.
>
>La versione 2.3.0 dell’SDK richiede Xcode 12.0 o versione successiva e, se applicabile, Cocoapods 1.10.0 o versione successiva.

* Ogni volta che si fa riferimento a un file di libreria binario, si deve usare la sua forma sostitutiva XCFramework:
   * MediaSDK.a > MediaSDK.xcframework
   * MediaSDK_TV.a > MediaSDKTV.xcframework
* Se nel progetto devi aggiungere manualmente codice in formato Adobe XCFrameworks, questo non deve essere incorporato.

1. Aggiungi l&#39;SDK [scaricato](/help/sdk-implement/download-sdks.md#download-2x-sdks) per file multimediali al tuo progetto.

   1. Verificare che nella directory `libs` siano presenti i seguenti componenti software:

      * `ADBMediaHeartbeat.h`: Il file di intestazione Objective-C utilizzato per le API di tracciamento heartbeat iOS.
      * `ADBMediaHeartbeatConfig.h`: Il file di intestazione Objective-C per la configurazione dell&#39;SDK.
      * `MediaSDK.a`: fat binary abilitato per bitcode contenente le build della libreria per dispositivi (armv7, armv7s, arm64) e simulatori (i386 e x86_64) iOS.

         Se la destinazione sarà un&#39;app iOS, il binary deve essere collegato.

      * `MediaSDK_TV.a`: Un fat binary abilitato per bitcode contenente le build della libreria per i nuovi dispositivi Apple TV (arm64) e simulatori (x86_64).

         Il binario deve essere collegato quando la destinazione è destinata a un&#39;app Apple TV (tvOS).
   1. Aggiungi la libreria al progetto:

      1. Avvia l&#39;IDE di Xcode e apri la tua app.
      1. In **[!UICONTROL Project Navigator]**, trascina la directory `libs` e rilasciala sotto il progetto.

      1. Assicurarsi che la casella di controllo **[!UICONTROL Copy Items if Needed]** sia selezionata, che la casella di controllo **[!UICONTROL Create Groups]** sia selezionata e che nessuna delle caselle di controllo in **[!UICONTROL Add to Target]** sia selezionata.

         ![](assets/choose-options_ios.png)

      1. Fai clic su **[!UICONTROL Finish]**.
      1. In **[!UICONTROL Project Navigator]**, seleziona l&#39;app e seleziona le destinazioni.
      1. Collegare i framework e le librerie richiesti nella sezione **[!UICONTROL Linked Frameworks]** e **[!UICONTROL Libraries]** della scheda **[!UICONTROL General]**.

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

1. Create un&#39;istanza `ADBMediaHeartbeatConfig`.

   Questa sezione descrive i parametri di configurazione `MediaHeartbeat` e consente di impostare valori di configurazione corretti sull&#39;istanza `MediaHeartbeat` per un monitoraggio accurato.

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

1. Implementa il protocollo `ADBMediaHeartbeatDelegate`.

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

1. Utilizzare `ADBMediaHeartBeatConfig` e `ADBMediaHeartBeatDelegate` per creare l&#39;istanza `ADBMediaHeartbeat`.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate:
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Assicurarsi che l&#39;istanza `ADBMediaHeartbeat` sia accessibile e che *non venga deallocata fino alla fine della sessione*. Questa istanza verrà utilizzata per tutti i seguenti eventi di tracciamento.

## Migrazione dalla versione 1.x alla 2.x in iOS {#migrate-to-two-x}

Nella versione 2.x, tutti i metodi pubblici sono consolidati nella classe `ADBMediaHeartbeat` per semplificare gli sviluppatori. Tutte le configurazioni sono state consolidate nella classe `ADBMediaHeartbeatConfig`.

Per ulteriori informazioni sulla migrazione da 1.x a 2.x, vedere [Migrazione VHL 1.x a 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## Configurare un&#39;app nativa per tvOS

Con il rilascio della nuova Apple TV, ora è possibile creare applicazioni da eseguire nell&#39;ambiente tvOS nativo. Potete creare un&#39;app puramente nativa, utilizzando diversi framework disponibili in iOS, oppure potete creare l&#39;app utilizzando modelli XML e JavaScript. A partire da MediaSDK versione 2.0, è disponibile il supporto per tvOS. Per ulteriori informazioni su tvOS, vedere [tvOS Developer site.](https://developer.apple.com/tvos/)

Effettuare le seguenti operazioni nel progetto Xcode. Questa guida viene scritta partendo dal presupposto che il progetto abbia una destinazione che sia un&#39;app Apple TV per tvOS:

1. Trascinate il file libreria `VideoHeartbeat_TV.a` nella cartella `lib` del progetto.

1. Nella scheda **[!UICONTROL Build Phases]** della destinazione dell&#39;app tvOS, espandi la sezione **[!UICONTROL Link Binary with Libraries]** e aggiungi le seguenti librerie:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`
