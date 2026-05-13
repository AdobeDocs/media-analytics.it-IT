---
title: Come impostare Media SDK su Android
description: Segui questi passaggi per configurare l’applicazione Media SDK su Android.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
exl-id: 261445bf-3c8b-4658-891d-9a878e0b26ea
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/re7nZLD9IwvufJGicWLArSwdIi6h518q3ZMDf6oqaCI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 435
ht-degree: 86%

---

# Configurazione Android{#set-up-android}

Scopri come impostare servizi multimediali in streaming per dispositivi Android.

>[!IMPORTANT]
>
>Con la fine del supporto per gli SDK della versione 4 per dispositivi mobili il 31 agosto 2021, Adobe terminerà anche il supporto per l’SDK di Media Analytics per iOS e Android.  Per ulteriori informazioni, consulta [Domande frequenti relative alla fine del supporto dell’SDK di Media Analytics](/help/additional-resources/end-of-support-faqs.md).


## Prerequisiti

* **Ottieni parametri di configurazione validi per Media SDK**
Questi parametri possono essere ottenuti da un rappresentante di Adobe dopo la configurazione dell’account di analisi.
* **Implementa ADBMobile per Android nella tua applicazione**
Per ulteriori informazioni sulla documentazione di Adobe Mobile SDK, consulta [Android SDK 4.x per soluzioni Experience Cloud.](https://experienceleague.adobe.com/docs/mobile-services/android/overview.html?lang=it)

* **Fornisci le seguenti funzionalità nel lettore multimediale:**
   * *API per abbonarsi agli eventi del lettore*: Media SDK richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.
   * *API che fornisce informazioni sul lettore* - Queste informazioni includono dettagli quali il nome del supporto e la posizione della testina di riproduzione.

## Implementazione SDK

1. Aggiungi il Media SDK scaricato al progetto.

   1. Espandi il file zip Android (ad es. `MediaSDK-android-v2.*.zip`).
   1. Verifica che il file `MediaSDK.jar` esista nella directory `libs/`.

   1. Aggiungi la libreria al progetto.

      **IDEA IntelliJ:**

      1. Fai clic con il pulsante destro del mouse sul progetto nel pannello **[!UICONTROL Project navigation]**.
      1. Seleziona **[!UICONTROL Open Module Settings]**.
      1. Sotto **[!UICONTROL Project Settings]**, seleziona **[!UICONTROL Libraries]**.

      1. Fai clic su **[!UICONTROL +]** per aggiungere una nuova libreria.
      1. Seleziona **[!UICONTROL Java]** e naviga fino al file `MediaSDK.jar`.

      1. Seleziona i moduli nei quali intendi usare la libreria mobile.
      1. Fai clic su **[!UICONTROL Apply]**, quindi su **[!UICONTROL OK]** per chiudere la finestra Impostazioni modulo.

      **Eclipse:**

      1. Nell’IDE Eclipse, fai clic con il pulsante destro del mouse sul nome del progetto.
      1. Fai clic su  **[!UICONTROL Build Path]** > **[!UICONTROL Add External Archives]**.
      1. Seleziona `MediaSDK.jar`.
      1. Fai clic su **[!UICONTROL Open]**.
      1. Fai nuovamente clic con il pulsante destro del mouse sul progetto e quindi su **[!UICONTROL Build Path]** > **[!UICONTROL Configure Build Path]**.
      1. Fai clic sulle schede **[!UICONTROL Order]** e **[!UICONTROL Export]**.

      1. Assicurati che il file `MediaSDK.jar` sia selezionato.

1. Importa la libreria.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat;
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate;
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig;
   import com.adobe.primetime.va.simple.MediaObject;
   ```

1. Crea l’istanza `MediaHeartbeatConfig`.

   Esempio di inizializzazione `MediaHeartbeatConfig`:

   ```java
   // Media Heartbeat Initialization
   config.trackingServer = _<SAMPLE_HEARTBEAT_TRACKING_SERVER>_;
   config.channel = <SAMPLE_HEARTBEAT_CHANNEL>;
   config.appVersion = <SAMPLE_HEARTBEAT_SDK_VERSION>;
   config.ovp =  <SAMPLE_HEARTBEAT_OVP_NAME>;
   config.playerName = <SAMPLE_PLAYER_NAME>;
   config.ssl = <true/false>;
   config.debugLogging = <true/false>;
   ```

1. Implementa l’interfaccia `MediaHeartbeatDelegate`.

   ```java
   public class VideoAnalyticsProvider implements Observer, MediaHeartbeatDelegate{}
   ```

   ```java
   // Replace <bitrate>, <startupTime>, <fps>, and  
   // <droppeFrames> with the current playback QoS values.  
   @Override
   public MediaObject getQoSObject() {
       return MediaHeartbeat.createQoSObject(<bitrate>,  
                                             <startupTime>,  
                                             <fps>,  
                                             <droppedFrames>);
   }
   
   //Replace <currentPlaybackTime> with the video player current playback time
   @Override
   public Double getCurrentPlaybackTime() {
       return <currentPlaybackTime>;
   }
   ```

1. Crea l’istanza `MediaHeartbeat`.

   Utilizza le istanze `MediaHeartbeatConfig` e `MediaHertbeatDelegate` per creare la `MediaHeartbeat`.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Assicurati che la tua istanza `MediaHeartbeat` sia accessibile e *non venga deallocata fino alla fine della sessione*. Questa istanza verrà utilizzata per tutti gli eventi di tracciamento seguenti.

**Aggiunta di autorizzazioni app**

L’app che utilizza Media SDK richiede le seguenti autorizzazioni per inviare dati nelle chiamate di tracciamento:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Per aggiungere queste autorizzazioni, aggiungi le seguenti righe al file `AndroidManifest.xml`, che si trova nella directory di progetto dell’applicazione:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migrazione dalla versione 1.x alla versione 2.x in Android**

Nelle versioni 2.x, tutti i metodi pubblici sono consolidati in `com.adobe.primetime.va.simple.MediaHeartbeat` per semplificare lo sviluppo. Inoltre, tutte le configurazioni sono ora consolidate nella classe `com.adobe.primetime.va.simple.MediaHeartbeatConfig`.

Per informazioni sulla migrazione dalla versione 1.x alla versione 2.x, consulta la documentazione dell’implementazione legacy.
