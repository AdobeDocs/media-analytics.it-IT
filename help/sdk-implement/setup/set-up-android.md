---
seo-title: Configurare Android
title: Configurare Android
uuid: 3 ffe 3276-a 104-4182-9220-038729 e 9 f 3 d 5
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Set up Android{#set-up-android}

## Prerequisiti

* **Ottenete parametri di configurazione validi per Media SDK**
Questi parametri possono essere ottenuti da un rappresentante Adobe dopo aver configurato il vostro account Analytics.
* **Implementa adbmobile per Android nell'applicazione**
Per ulteriori informazioni sulla documentazione SDK di Adobe Mobile, consulta [Android SDK 4. x per soluzioni Experience Cloud.](https://marketing.adobe.com/resources/help/en_US/mobile/android/)
* **Fornite le seguenti funzionalità nel lettore multimediale:**
   * *API per l'iscrizione agli eventi del lettore* - L'SDK di Media richiede che venga chiamato un set di API semplici quando si verificano eventi nel lettore.
   * *API che fornisce informazioni* sul lettore: informazioni dettagliate quali il nome del supporto e la posizione della testina di riproduzione.

## Implementazione SDK

1. Add your [downloaded](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) Media SDK to your project.

   1. Expand the Android zip file (e.g., `MediaSDK-android-v2.*.zip`).
   1. Verify that the `MediaSDK.jar` file exists in the `libs/` directory.

   1. Aggiungete la libreria al progetto.

      **Intellij IDEA:**

      1. Right click your project in the **[!UICONTROL Project navigation]** panel.
      1. Select **[!UICONTROL Open Module Settings]**.
      1. Under **[!UICONTROL Project Settings]**, select **[!UICONTROL Libraries]**.

      1. Click **[!UICONTROL +]** to add a new library.
      1. Select **[!UICONTROL Java]** and navigate to the `MediaSDK.jar` file.

      1. Selezionate i moduli in cui intendete utilizzare la libreria mobile.
      1. Click **[!UICONTROL Apply]** and then **[!UICONTROL OK]** to close the Module Settings window.
      **Eclipse:**

      1. Nell'IDE Eclipse, fai clic con il pulsante destro del mouse sul nome del progetto.
      1. Click  **[!UICONTROL Build Path]** &gt; **[!UICONTROL Add External Archives]** .
      1. Seleziona `MediaSDK.jar`.
      1. Fai clic su **[!UICONTROL Open]**.
      1. Right-click the project again, and click  **[!UICONTROL Build Path]** &gt; **[!UICONTROL Configure Build Path]** .
      1. Click the **[!UICONTROL Order]** and **[!UICONTROL Export]** tabs.

      1. Ensure that the `MediaSDK.jar` file is selected.


1. Importa la libreria.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat; 
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate; 
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig; 
   import com.adobe.primetime.va.simple.MediaObject; 
   ```

1. Create the `MediaHeartbeatConfig` instance.

   Esempio `MediaHeartbeatConfig` di inizializzazione:

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

1. Implement the `MediaHeartbeatDelegate` interface.

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

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` instance and the `MediaHertbeatDelegate` instance to create the `MediaHeartbeat` instance.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance 
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and *does not get deallocated until the end of the session*. Questa istanza verrà utilizzata per tutti i seguenti eventi di tracciamento.

**Aggiunta delle autorizzazioni dell'app**

L'app che utilizza Media SDK richiede le seguenti autorizzazioni per inviare dati nelle chiamate di tracciamento:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

To add these permissions, add the following lines to your `AndroidManifest.xml` file in the application project directory:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migrazione dalla versione 1. x alla 2. x in Android**

In versions 2.x, all of the public methods are consolidated into the `com.adobe.primetime.va.simple.MediaHeartbeat` class to make it easier on developers. Also, all configs are now consolidated into the `com.adobe.primetime.va.simple.MediaHeartbeatConfig` class.

For detailed information about migrating from 1.x to 2.x, see [mig-1x-2x-overview.md.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
