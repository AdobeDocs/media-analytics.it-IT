---
title: Configurazione Android
description: Configurazione dell’applicazione Media SDK per l’implementazione su Android.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
translation-type: tm+mt
source-git-commit: 300eb77858296f0246a2cb484386c0dcdf8b87b9
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 10%

---


# Configurazione Android{#set-up-android}

>[!IMPORTANT]
>
>Con la fine del supporto per gli SDK della versione 4 per dispositivi mobili il 31 agosto 2021, Adobe interromperà anche il supporto per l’SDK di Media Analytics per iOS e Android.  Per ulteriori informazioni, consultate Domande frequenti relative alla fine del supporto per l’SDK di [Media Analytics](/help/sdk-implement/end-of-support-faqs.md).


## Prerequisiti

* **Ottenete parametri di configurazione validi per Media SDK** Questi parametri possono essere ottenuti da un rappresentante Adobe dopo che avete configurato il vostro account di analisi.
* **Implementa ADBMobile per Android nella tua applicazione** Per ulteriori informazioni sulla documentazione SDK per Adobe Mobile, consulta SDK 4.x per [Android per le soluzioni Experience Cloud.](https://docs.adobe.com/content/help/it-IT/mobile-services/android/overview.html)

* **Fornite le seguenti funzionalità nel lettore multimediale:**
   * *Un&#39;API per iscriversi agli eventi* del lettore - L&#39;SDK di Media richiede che venga chiamato un set di API semplici quando si verificano eventi nel lettore.
   * *API che fornisce informazioni* sul lettore - Queste informazioni includono dettagli quali il nome del supporto e la posizione della testina di riproduzione.

## Implementazione SDK

1. Aggiungi l’SDK per file multimediali [scaricato](/help/sdk-implement/download-sdks.md#download-2x-sdks) al progetto.

   1. Espandete il file zip Android (ad esempio, `MediaSDK-android-v2.*.zip`).
   1. Verificate che il `MediaSDK.jar` file esista nella `libs/` directory.

   1. Aggiungi la libreria al progetto.

      **IDEA IntelliJ:**

      1. Right click your project in the **[!UICONTROL Project navigation]** panel.
      1. Select **[!UICONTROL Open Module Settings]**.
      1. In **[!UICONTROL Project Settings]**, selezionare **[!UICONTROL Libraries]**.

      1. Fate clic **[!UICONTROL +]** per aggiungere una nuova libreria.
      1. Seleziona **[!UICONTROL Java]** e naviga fino al file `MediaSDK.jar`.

      1. Selezionate i moduli in cui intendete utilizzare la libreria mobile.
      1. Click **[!UICONTROL Apply]** and then **[!UICONTROL OK]** to close the Module Settings window.
      **Eclipse:**

      1. Nell’IDE Eclipse, fai clic con il pulsante destro del mouse sul nome del progetto.
      1. Fai clic su  **[!UICONTROL Build Path]** > **[!UICONTROL Add External Archives]** .
      1. Select `MediaSDK.jar`.
      1. Fai clic su **[!UICONTROL Open]**.
      1. Fate nuovamente clic con il pulsante destro del mouse sul progetto e fate clic su **[!UICONTROL Build Path]** > **[!UICONTROL Configure Build Path]** .
      1. Fare clic sulle schede **[!UICONTROL Order]** e **[!UICONTROL Export]** .

      1. Assicurarsi che il `MediaSDK.jar` file sia selezionato.


1. Importa la libreria.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat;
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate;
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig;
   import com.adobe.primetime.va.simple.MediaObject;
   ```

1. Create l’ `MediaHeartbeatConfig` istanza.

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

1. Implementare l&#39; `MediaHeartbeatDelegate` interfaccia.

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

1. Create l’ `MediaHeartbeat` istanza.

   Utilizzate l&#39; `MediaHeartbeatConfig` istanza e l&#39; `MediaHertbeatDelegate` istanza per creare l&#39; `MediaHeartbeat` istanza.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Accertatevi che l’ `MediaHeartbeat` istanza sia accessibile e che *non venga deallocata fino alla fine della sessione*. Questa istanza verrà utilizzata per tutti i seguenti eventi di tracciamento.

**Aggiunta di autorizzazioni per l&#39;app**

L’app che utilizza Media SDK richiede le seguenti autorizzazioni per inviare dati nelle chiamate di tracciamento:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

To add these permissions, add the following lines to your `AndroidManifest.xml` file in the application project directory:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migrazione dalla versione 1.x alla 2.x in Android**

Nelle versioni 2.x, tutti i metodi pubblici sono consolidati nella `com.adobe.primetime.va.simple.MediaHeartbeat` classe per semplificare gli sviluppatori. Inoltre, tutte le configurazioni sono ora consolidate nella `com.adobe.primetime.va.simple.MediaHeartbeatConfig` classe.

Per informazioni dettagliate sulla migrazione da 1.x a 2.x, consultate [mig-1x-2x-overview.md.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
