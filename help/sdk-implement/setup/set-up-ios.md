---
title: Come configurare il Media SDK su iOS
description: Segui questi passaggi per configurare l’applicazione Media SDK su iOS.
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
exl-id: fe7662b5-1700-4bd6-b542-66aa8493459d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 15%

---

# Configurazione iOS{#set-up-ios}

Scopri come configurare Streaming Media Analytics per dispositivi iOS.

>[!IMPORTANT]
>
>Con la fine del supporto per gli SDK della versione 4 per dispositivi mobili il 31 agosto 2021, Adobe terminerà anche il supporto per l’SDK di Media Analytics per iOS e Android.  Per ulteriori informazioni, consulta [Domande frequenti sulla fine del supporto dell’SDK di Media Analytics](/help/sdk-implement/end-of-support-faqs.md).

## Prerequisiti

* **Ottenere parametri di configurazione validi per Media**
SDKTquesti parametri possono essere ottenuti da un rappresentante di Adobe dopo aver configurato il tuo account di analisi.
* **Implementa ADBMobile per iOS nell’**
applicazione. Per ulteriori informazioni sull’SDK di Adobe Mobile, consulta SDK 4.x per  [iOS per le soluzioni Experience Cloud.](https://experienceleague.adobe.com/docs/mobile-services/ios/overview.html?lang=it)

   >[!IMPORTANT]
   >
   >A partire da iOS 9, Apple ha introdotto una funzione chiamata App Transport Security (ATS). Questa funzione mira a migliorare la sicurezza della rete assicurando che le app utilizzino solo protocolli e crittografie standard del settore. Questa funzione è abilitata per impostazione predefinita, ma disponi di opzioni di configurazione che ti forniscono la possibilità di lavorare con ATS. Per informazioni dettagliate su ATS, consulta [App Transport Security.](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/app-transport-security.html)

* **Fornisci le seguenti funzionalità nel lettore multimediale:**

   * _Un’API per abbonarti agli eventi_  del lettore: l’SDK per contenuti multimediali richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.
   * _API che fornisce informazioni_  sul lettore. Queste informazioni includono dettagli quali il nome del contenuto multimediale e la posizione della testina di riproduzione.

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

1. Aggiungi il tuo [scaricato](/help/sdk-implement/download-sdks.md#download-2x-sdks) Media SDK al tuo progetto.

   1. Verifica che nella directory `libs` siano presenti i seguenti componenti software:

      * `ADBMediaHeartbeat.h`: Il file di intestazione Objective-C utilizzato per le API di tracciamento heartbeat iOS.
      * `ADBMediaHeartbeatConfig.h`: Il file di intestazione Objective-C per la configurazione dell&#39;SDK.
      * `MediaSDK.a`: fat binary abilitato per bitcode contenente le build della libreria per dispositivi (armv7, armv7s, arm64) e simulatori (i386 e x86_64) iOS.

         Se la destinazione sarà un&#39;app iOS, il binary deve essere collegato.

      * `MediaSDK_TV.a`: fat binary abilitato per bitcode contenente le build della libreria per dispositivi (arm64) e simulatori (x86_64) Apple TV.

         Se la destinazione sarà un&#39;app Apple TV (tvOS), il binario deve essere collegato.
   1. Aggiungi la libreria al progetto:

      1. Avvia l&#39;IDE di Xcode e apri la tua app.
      1. In **[!UICONTROL Project Navigator]**, trascina la directory `libs` e rilasciala sotto al tuo progetto.

      1. Assicurati che la casella di controllo **[!UICONTROL Copy Items if Needed]** sia selezionata, che sia selezionato **[!UICONTROL Create Groups]** e che nessuna delle caselle di controllo in **[!UICONTROL Add to Target]** sia selezionata.

         ![](assets/choose-options_ios.png)

      1. Fai clic su **[!UICONTROL Finish]**.
      1. In **[!UICONTROL Project Navigator]**, seleziona l’app e seleziona le destinazioni.
      1. Collega i framework e le librerie richiesti nella sezione **[!UICONTROL Linked Frameworks]** e **[!UICONTROL Libraries]** della scheda **[!UICONTROL General]** .

         **Destinazioni di app iOS:**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**

         **Destinazioni Apple TV (tvOS):**

         * **AdobeMobileLibrary_TV.a**
         * **MediaSDK_TV.a**
         * **libsqlite3.0.tbd**
         * **SystemConfiguration.framework**
      1. Verifica che l’app possa essere generata senza errori.




1. Importa la libreria.

   ```
   #import "ADBMediaHeartbeat.h"
   #import "ADBMediaHeartbeatConfig.h"
   ```

1. Crea un&#39;istanza `ADBMediaHeartbeatConfig`.

   Questa sezione ti aiuta a comprendere i parametri di configurazione `MediaHeartbeat` e a impostare i valori di configurazione corretti sull&#39;istanza `MediaHeartbeat` per un monitoraggio accurato.

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

1. Implementa il protocollo `ADBMediaHeartbeatDelegate` .

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

1. Utilizza i valori `ADBMediaHeartBeatConfig` e `ADBMediaHeartBeatDelegate` per creare l&#39;istanza `ADBMediaHeartbeat`.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate:
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Assicurati che l&#39;istanza `ADBMediaHeartbeat` sia accessibile e che *non venga deassegnata fino alla fine della sessione*. Questa istanza verrà utilizzata per tutti i seguenti eventi di tracciamento.

## Migrazione dalla versione 1.x alla versione 2.x in iOS {#migrate-to-two-x}

Nella versione 2.x, tutti i metodi pubblici sono consolidati nella classe `ADBMediaHeartbeat` per facilitare gli sviluppatori. Tutte le configurazioni sono state consolidate nella classe `ADBMediaHeartbeatConfig` .

Per ulteriori informazioni sulla migrazione da 1.x a 2.x, consulta [Migrazione da VHL 1.x a 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## Configurare un&#39;app nativa per tvOS

Con il rilascio della nuova Apple TV, è ora possibile creare applicazioni da eseguire nell&#39;ambiente nativo tvOS. Puoi creare un’app puramente nativa, utilizzando uno qualsiasi dei diversi framework disponibili in iOS, oppure puoi creare l’app utilizzando modelli XML e JavaScript. A partire da MediaSDK versione 2.0, è disponibile il supporto per tvOS. Per ulteriori informazioni su tvOS, consulta [sito per sviluppatori tvOS.](https://developer.apple.com/tvos/)

Esegui i seguenti passaggi nel progetto Xcode. Questa guida viene scritta presupponendo che il progetto abbia una destinazione che sia un&#39;app Apple TV per tvOS:

1. Trascina il file della libreria `VideoHeartbeat_TV.a` nella cartella `lib` del progetto.

1. Nella scheda **[!UICONTROL Build Phases]** della destinazione dell&#39;app tvOS, espandi la sezione **[!UICONTROL Link Binary with Libraries]** e aggiungi le seguenti librerie:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`
