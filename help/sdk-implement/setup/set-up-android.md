---
title: Come impostare Media SDK su Android
description: Segui questi passaggi per configurare l’applicazione Media SDK su Android.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
exl-id: 261445bf-3c8b-4658-891d-9a878e0b26ea
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 9%

---

# Configurazione Android{#set-up-android}

>[!IMPORTANT]
>
>Con la fine del supporto per gli SDK della versione 4 per dispositivi mobili il 31 agosto 2021, Adobe terminerà anche il supporto per l’SDK di Media Analytics per iOS e Android.  Per ulteriori informazioni, consulta [Domande frequenti sulla fine del supporto dell’SDK di Media Analytics](/help/sdk-implement/end-of-support-faqs.md).


## Prerequisiti

* **Ottenere parametri di configurazione validi per Media**
SDKTquesti parametri possono essere ottenuti da un rappresentante di Adobe dopo aver configurato il tuo account di analisi.
* **Implementa ADBMobile per Android nell’**
applicazione. Per ulteriori informazioni sull’SDK di Adobe Mobile, consulta SDK 4.x per  [Android per le soluzioni Experience Cloud.](https://experienceleague.adobe.com/docs/mobile-services/android/overview.html?lang=it)

* **Fornisci le seguenti funzionalità nel lettore multimediale:**
   * *Un’API per abbonarti agli eventi*  del lettore: l’SDK per contenuti multimediali richiede di chiamare un set di API semplici quando si verificano eventi nel lettore.
   * *API che fornisce informazioni*  sul lettore. Queste informazioni includono dettagli quali il nome del contenuto multimediale e la posizione della testina di riproduzione.

## Implementazione SDK

1. Aggiungi il tuo [scaricato](/help/sdk-implement/download-sdks.md#download-2x-sdks) Media SDK al tuo progetto.

   1. Espandi il file zip Android (ad esempio, `MediaSDK-android-v2.*.zip`).
   1. Verifica che il file `MediaSDK.jar` esista nella directory `libs/`.

   1. Aggiungi la libreria al progetto.

      **IDEA IntelliJ:**

      1. Fai clic con il pulsante destro del mouse sul progetto nel pannello **[!UICONTROL Project navigation]** .
      1. Select **[!UICONTROL Open Module Settings]**.
      1. In **[!UICONTROL Project Settings]**, selezionare **[!UICONTROL Libraries]**.

      1. Fai clic su **[!UICONTROL +]** per aggiungere una nuova libreria.
      1. Seleziona **[!UICONTROL Java]** e naviga fino al file `MediaSDK.jar`.

      1. Seleziona i moduli in cui intendi utilizzare la libreria mobile.
      1. Fare clic su **[!UICONTROL Apply]** e quindi su **[!UICONTROL OK]** per chiudere la finestra Impostazioni modulo.

      **Eclipse:**

      1. Nell’IDE Eclipse, fai clic con il pulsante destro del mouse sul nome del progetto.
      1. Fai clic su  **[!UICONTROL Build Path]** > **[!UICONTROL Add External Archives]** .
      1. Selezionare `MediaSDK.jar`.
      1. Fai clic su **[!UICONTROL Open]**.
      1. Fai nuovamente clic con il pulsante destro del mouse sul progetto e fai clic su **[!UICONTROL Build Path]** > **[!UICONTROL Configure Build Path]** .
      1. Fare clic sulle schede **[!UICONTROL Order]** e **[!UICONTROL Export]**.

      1. Assicurati che il file `MediaSDK.jar` sia selezionato.


1. Importa la libreria.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat;
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate;
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig;
   import com.adobe.primetime.va.simple.MediaObject;
   ```

1. Crea l&#39;istanza `MediaHeartbeatConfig` .

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

1. Implementa l&#39;interfaccia `MediaHeartbeatDelegate` .

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

1. Crea l&#39;istanza `MediaHeartbeat` .

   Utilizza l&#39;istanza `MediaHeartbeatConfig` e l&#39;istanza `MediaHertbeatDelegate` per creare l&#39;istanza `MediaHeartbeat`.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Assicurati che l&#39;istanza `MediaHeartbeat` sia accessibile e che *non venga deassegnata fino alla fine della sessione*. Questa istanza verrà utilizzata per tutti i seguenti eventi di tracciamento.

**Aggiunta di autorizzazioni app**

L&#39;app che utilizza Media SDK richiede le seguenti autorizzazioni per inviare dati nelle chiamate di tracciamento:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Per aggiungere queste autorizzazioni, aggiungi le seguenti righe al file `AndroidManifest.xml` nella directory di progetto dell&#39;applicazione:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migrazione dalla versione 1.x alla versione 2.x in Android**

Nelle versioni 2.x, tutti i metodi pubblici sono consolidati nella classe `com.adobe.primetime.va.simple.MediaHeartbeat` per facilitare gli sviluppatori. Inoltre, tutte le configurazioni sono ora consolidate nella classe `com.adobe.primetime.va.simple.MediaHeartbeatConfig` .

Per informazioni dettagliate sulla migrazione da 1.x a 2.x, consulta [mig-1x-2x-overview.md.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
