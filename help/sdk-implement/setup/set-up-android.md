---
seo-title: Configurare Android
title: Configurare Android
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
translation-type: tm+mt
source-git-commit: a3a81609046ab5e3c84fe4bf99c92c3dabc58247

---


# Configurare Android{#set-up-android}

## Prerequisiti

* **Ottenete parametri di configurazione validi per Media SDK** Questi parametri possono essere ottenuti da un rappresentante Adobe dopo la configurazione dell'account di analisi.
* **Implementa ADBMobile per Android nella tua applicazione** Per ulteriori informazioni sulla documentazione SDK per Adobe Mobile, consulta [Android SDK 4.x per le soluzioni Experience Cloud.](https://marketing.adobe.com/resources/help/en_US/mobile/android/)
* **Fornite le seguenti funzionalità nel lettore multimediale:**
   * *Un'API per iscriversi agli eventi* del lettore - L'SDK di Media richiede che venga chiamato un set di API semplici quando si verificano eventi nel lettore.
   * *API che fornisce informazioni* sul lettore - Queste informazioni includono dettagli quali il nome del supporto e la posizione della testina di riproduzione.

## Implementazione SDK

1. Aggiungi l’SDK per file multimediali [scaricato](/help/sdk-implement/download-sdks.md#download-2x-sdks) al progetto.

   1. Espandete il file zip Android (ad esempio, `MediaSDK-android-v2.*.zip`).
   1. Verificate che il `MediaSDK.jar` file esista nella `libs/` directory.

   1. Aggiungi la libreria al progetto.

      **IDEA IntelliJ:**

      1. Right click your project in the **[!UICONTROL Project navigation]** panel.
      1. Seleziona **[!UICONTROL Open Module Settings]**.
      1. In **[!UICONTROL Project Settings]**, selezionare **[!UICONTROL Libraries]**.

      1. Click **[!UICONTROL +]** to add a new library.
      1. Seleziona **[!UICONTROL Java]** e naviga fino al file `MediaSDK.jar`.

      1. Selezionate i moduli in cui intendete utilizzare la libreria mobile.
      1. Click **[!UICONTROL Apply]** and then **[!UICONTROL OK]** to close the Module Settings window.
      **Eclipse:**

      1. Nell’IDE Eclipse, fai clic con il pulsante destro del mouse sul nome del progetto.
      1. Fai clic su  **[!UICONTROL Build Path]** &gt; **[!UICONTROL Add External Archives]** .
      1. Seleziona `MediaSDK.jar`.
      1. Fai clic su **[!UICONTROL Open]**.
      1. Fate nuovamente clic con il pulsante destro del mouse sul progetto e fate clic su **[!UICONTROL Build Path]** &gt; **[!UICONTROL Configure Build Path]** .
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

1. Implementare l' `MediaHeartbeatDelegate` interfaccia.

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

   Utilizzate l' `MediaHeartbeatConfig` istanza e l' `MediaHertbeatDelegate` istanza per creare l' `MediaHeartbeat` istanza.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance 
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Accertatevi che l’ `MediaHeartbeat` istanza sia accessibile e che *non venga deallocata fino alla fine della sessione*. Questa istanza verrà utilizzata per tutti i seguenti eventi di tracciamento.

**Aggiunta di autorizzazioni per l'app**

L’app che utilizza Media SDK richiede le seguenti autorizzazioni per inviare dati nelle chiamate di tracciamento:

* `INTERNET`
* `ACCESS_NETWORK_STATE`

To add these permissions, add the following lines to your `AndroidManifest.xml` file in the application project directory:

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migrazione dalla versione 1.x alla 2.x in Android**

Nelle versioni 2.x, tutti i metodi pubblici sono consolidati nella `com.adobe.primetime.va.simple.MediaHeartbeat` classe per semplificare gli sviluppatori. Inoltre, tutte le configurazioni sono ora consolidate nella `com.adobe.primetime.va.simple.MediaHeartbeatConfig` classe.

Per informazioni dettagliate sulla migrazione da 1.x a 2.x, consultate [mig-1x-2x-overview.md.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
