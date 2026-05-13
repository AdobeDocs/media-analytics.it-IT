---
title: Configurare Media SDK su iOS
description: Segui questi passaggi per configurare l’applicazione Media SDK su iOS.
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
exl-id: fe7662b5-1700-4bd6-b542-66aa8493459d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/UP1biESuMpPqJNXKmEG-RU-8iBIHJcVZ87N0EsuZ1hI
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 763
ht-degree: 88%

---

# Configurazione iOS{#set-up-ios}

Scopri come configurare i servizi di streaming media per i dispositivi iOS.

>[!IMPORTANT]
>
>Con la fine del supporto per gli SDK della versione 4 per dispositivi mobili il 31 agosto 2021, Adobe terminerà anche il supporto per l’SDK di Media Analytics per iOS e Android.  Per ulteriori informazioni, consulta [Domande frequenti relative alla fine del supporto dell’SDK di Media Analytics](/help/additional-resources/end-of-support-faqs.md).

## Prerequisiti

* **Ottieni parametri di configurazione validi per Media SDK**
Questi parametri possono essere ottenuti da un rappresentante di Adobe dopo la configurazione dell’account di analisi.
* **Implementa ADBMobile per iOS nella tua applicazione**
Per ulteriori informazioni sulla documentazione di Adobe Mobile SDK, consulta [iOS SDK 4.x per soluzioni Experience Cloud.](https://experienceleague.adobe.com/docs/mobile-services/ios/overview.html?lang=it)

  >[!IMPORTANT]
  >
  >A partire da iOS 9, Apple ha introdotto una funzione denominata App Transport Security (ATS). Questa funzione mira a migliorare la sicurezza della rete assicurando che le app utilizzino solo protocolli e cifrature standard del settore. Questa funzione è abilitata per impostazione predefinita, ma disponi di opzioni di configurazione per scegliere come lavorare con ATS. Per maggiori dettagli su ATS, consulta [App Transport Security.](https://experienceleague.adobe.com/docs/mobile-services/ios/config-ios/app-transport-security.html?lang=it)

* **Fornisci le seguenti funzionalità nel lettore multimediale:**

   * _API per abbonarsi agli eventi del lettore_: Media SDK richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.
   * _API che fornisce informazioni sul lettore_ - Queste informazioni includono dettagli quali il nome del supporto e la posizione della testina di riproduzione.

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

1. Aggiungi il Media SDK [scaricato](/help/getting-started/download-sdks.md) al progetto.

   1. Verifica che siano presenti i seguenti componenti software nella directory `libs`:

      * `ADBMediaHeartbeat.h`: file di intestazione Objective-C usato per le API di tracciamento heartbeat in iOS.
      * `ADBMediaHeartbeatConfig.h`: file di intestazione Objective-C per la configurazione dell’SDK.
      * `MediaSDK.a`: fat binary abilitato per bitcode contenente le build della libreria per dispositivi (armv7, armv7s, arm64) e simulatori (i386 e x86_64) iOS.

        Se la destinazione è un’app iOS, il binary deve essere collegato.

      * `MediaSDK_TV.a`: un fat binary abilitato per bitcode contenente le build della libreria per i nuovi dispositivi (arm64) e simulatori (x86_64) Apple TV.

        Se la destinazione è un’app per Apple TV (tvOS), il binary deve essere collegato.

   1. Aggiungi la libreria al progetto:

      1. Avvia l’IDE di Xcode e apri la tua app.
      1. In **[!UICONTROL Project Navigator]**, trascina la directory `libs` e rilasciala sotto al progetto.

      1. Assicurati che la casella di controllo **[!UICONTROL Copy Items if Needed]** sia selezionata, **[!UICONTROL Create Groups]** sia selezionato e nessuna delle caselle di controllo in **[!UICONTROL Add to Target]** sia selezionata.

      ![Scegli opzioni](assets/choose-options_ios.png)

      1. Fai clic su **[!UICONTROL Finish]**.
      1. In **[!UICONTROL Project Navigator]**, seleziona l’app e le destinazioni.
      1. Collega i framework e le librerie richiesti nelle sezioni **[!UICONTROL Linked Frameworks]** e **[!UICONTROL Libraries]** nella scheda **[!UICONTROL General]**.

         **Destinazioni di app iOS:**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**

         **Destinazioni Apple TV (tvOS):**

         * **AdobeMobileLibrary_TV.a**
         * **MediaSDK_TV.a**
         * **libsqlite3.0.tbd**
         * **ConfigurazioneSistema.framework**

      1. Verifica che l’app possa essere generata senza errori.

1. Importa la libreria.

   ```
   #import "ADBMediaHeartbeat.h"
   #import "ADBMediaHeartbeatConfig.h"
   ```

1. Crea un’istanza di `ADBMediaHeartbeatConfig`.

   Questa sezione descrive i parametri di configurazione di `MediaHeartbeat` e spiega come impostare i valori di configurazione corretti sull’istanza di `MediaHeartbeat` per un tracciamento accurato.

   Esempio di inizializzazione di `ADBMediaHeartbeatConfig`:

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

1. Utilizza `ADBMediaHeartBeatConfig` e `ADBMediaHeartBeatDelegate` per creare l’istanza di `ADBMediaHeartbeat`.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate:
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Assicurati che l’istanza di `ADBMediaHeartbeat` sia accessibile e che *non venga deallocata fino alla fine della sessione*. Questa istanza verrà utilizzata per tutti gli eventi di tracciamento seguenti.

## Migrazione dalla versione 1.x alla versione 2.x in iOS {#migrate-to-two-x}

Nella versione 2.x, tutti i metodi pubblici sono consolidati nella classe `ADBMediaHeartbeat` per semplificare il lavoro degli sviluppatori. Tutte le configurazioni sono state consolidate nella classe `ADBMediaHeartbeatConfig`.

Per informazioni sulla migrazione dalla versione 1.x alla versione 2.x, consulta la documentazione sull’implementazione legacy.

## Configurare un’app nativa per tvOS

Con il rilascio della nuova Apple TV, potrai creare applicazioni da eseguire nell’ambiente nativo tvOS. Puoi creare un’app esclusivamente nativa utilizzando uno dei numerosi framework disponibili in iOS, oppure puoi creare l’app utilizzando modelli XML e JavaScript. Il supporto per tvOS è disponibile a partire da MediaSDK versione 2.0. Per ulteriori informazioni su tvOS, consulta il [sito per sviluppatori tvOS.](https://developer.apple.com/tvos/)

Completa i seguenti passaggi nel progetto Xcode. Questa guida è stata scritta per un progetto il cui target è un’app Apple TV per il targeting di tvOS:

1. Trascina il file di libreria `VideoHeartbeat_TV.a` nella cartella `lib` del progetto.

1. Nella scheda **[!UICONTROL Build Phases]** della destinazione dell&#39;app tvOS, espandi la sezione **[!UICONTROL Link Binary with Libraries]** e aggiungi le seguenti librerie:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`
