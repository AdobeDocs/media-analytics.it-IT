---
title: Migrazione dall’SDK per file multimediali standalone ad Adobe Launch - Android
description: Istruzioni ed esempi di codice per facilitare la migrazione da Media SDK a Launch per Android.
translation-type: tm+mt
source-git-commit: bc896cc403923e2f31be7313ab2ca22c05893c45

---


# Migrazione dall’SDK per file multimediali standalone ad Adobe Launch - Android

## Configurazione

### SDK per file multimediali indipendenti

Nell’SDK per file multimediali indipendenti, puoi configurare il tracciamento nell’app e passarlo all’SDK quando crei il tracciatore.

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0.0";
config.ovp = "video-provider"; 
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeat tracker = new MediaHeartbeat(... , config);
```

### Avvia estensione

1. In Experience Platform Launch, fai clic sulla [!UICONTROL Extensions] scheda della proprietà mobile.
1. Nella [!UICONTROL Catalog] scheda, individua l’estensione Adobe Media Analytics for Audiences and Video e fai clic su [!UICONTROL Install].
1. Nella pagina delle impostazioni di estensione, configurate i parametri di tracciamento.
L’estensione Media utilizzerà i parametri configurati per il tracciamento.

![](assets/launch_config_mobile.png)

[Utilizzo delle estensioni mobili](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

## Creazione Tracker

### SDK per file multimediali indipendenti

Nell’SDK per file multimediali indipendenti potete creare manualmente l’ `MediaHeartbeatConfig` oggetto e configurare i parametri di tracciamento. Implementa l’interfaccia delegata che espone`getQoSObject()` e `getCurrentPlaybackTime()functions.`crea un’ `MediaHeartbeat` istanza per il tracciamento.

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0";
config.ovp = "video-provider"; 
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeatDelegate delegate = new MediaHeartbeatDelegate() {
    @Override 
    public MediaObject getQoSObject() {
        // When called should return the latest qos values.
        return MediaHeartbeat.createQoSObject(<bitrate>,  
                                              <startupTime>,  
                                              <fps>,  
                                              <droppedFrames>); 
    } 

    @Override 
    public Double getCurrentPlaybackTime() { 
        // When called should return the current player time in seconds.
        return <currentPlaybackTime>; 
    }

    MediaHeartbeat tracker = new MediaHeartbeat(delegate, config);
}
```

### Avvia estensione

[Riferimento API Media - Creazione di un Tracker multimediale](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

Prima di creare il tracciatore, è necessario registrare l’estensione del supporto e le estensioni dipendenti con il core mobile.

```java
// Register the extension once during app launch
try {
    // Media needs Identity and Analytics extension 
    // to function properly
    Identity.registerExtension();
    Analytics.registerExtension();

    // Initialize media extension.
    Media.registerExtension();                
    MobileCore.start(new AdobeCallback () {
        @Override
        public void call(Object o) {
            // Launch mobile property to pick extension settings.
            MobileCore.configureWithAppID("LAUNCH_MOBILE_PROPERTY");
        }
    });
} catch (InvalidInitException ex) {
    ...
}
```

Dopo aver registrato l’estensione del supporto, create il tracciatore utilizzando la seguente API.
Il tracciatore seleziona automaticamente la configurazione dalla proprietà di avvio configurata.

```java
Media.createTracker(new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker tracker) {
        // Use the instance for tracking media.
    }
});
```

## Aggiornamento dei valori Playhead e Quality of Experience.

### SDK per file multimediali indipendenti

Nell’SDK per file multimediali indipendenti, trasmetti un oggetto delegato che implementa l’interfaccia durante la creazione del`MediaHeartbeartDelegate` tracciatore.  L’implementazione deve restituire l’ultimo QoE e l’indicatore di riproduzione ogni volta che il tracciatore chiama i metodi e dell`getQoSObject()` ’ `getCurrentPlaybackTime()` interfaccia.

### Avvia estensione

L'implementazione deve aggiornare l'indicatore di riproduzione del lettore corrente chiamando il metodo esposto dal`updateCurrentPlayhead` tracciatore. Per un tracciamento accurato, devi chiamare questo metodo almeno una volta al secondo.

[Riferimento API Media - Aggiornamento del lettore corrente](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

L’implementazione deve aggiornare le informazioni QoE chiamando il `updateQoEObject`metodo esposto dal tracciatore. Ci aspettiamo che questo metodo venga chiamato ogni volta che si verificano modifiche nelle metriche di qualità.

[Riferimento API Media - Aggiornamento oggetto QoE](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

## Trasmissione di contenuti multimediali/metadati di annunci standard

### SDK per file multimediali indipendenti

* Metadati file multimediali standard:

   ```java
   MediaObject mediaInfo = 
     MediaHeartbeat.createMediaObject("media-name", 
                                      "media-id", 
                                      60D, 
                                      MediaHeartbeat.StreamType.VOD, 
                                      MediaHeartbeat.MediaType.Video);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardVideoMetadata = 
     new HashMap<String, String>(); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, 
                             "Sample Episode"); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, 
                             "Sample Show"); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, 
                             "Sample Season"); 
   mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardMediaMetadata, 
                      standardVideoMetadata);
   
   // Custom metadata keys
   HashMap<String, String> mediaMetadata = new HashMap<String, String>();
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* Metadati annuncio standard:

   ```java
   MediaObject adInfo = 
     MediaHeartbeat.createAdObject("ad-name", 
                                   "ad-id", 
                                   1L, 
                                   15D);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardAdMetadata = 
     new HashMap<String, String>(); 
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, 
                          "Sample Advertiser"); 
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, 
                          "Sample Campaign"); 
   adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, 
                   standardAdMetadata); 
   
   HashMap<String, String> adMetadata = 
     new HashMap<String, String>();
   adMetadata.put("affiliate", 
                  "Sample affiliate");
   
   tracker.trackEvent(MediaHeartbeat.Event.AdStart, 
                      adObject, 
                      adMetadata);
   ```

### Avvia estensione

* Metadati file multimediali standard:

   ```java
   HashMap<String, Object> mediaObject = 
     Media.createMediaObject("media-name", 
                             "media-id", 
                             60D, 
                             MediaConstants.StreamType.VOD, 
                             Media.MediaType.Video);
   
   HashMap<String, String> mediaMetadata = 
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.EPISODE, 
                     "Sample Episode");
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.SHOW, 
                     "Sample Show");
   
   // Custom metadata keys
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* Metadati annuncio standard:

   ```java
   HashMap<String, Object> adObject = 
     Media.createAdObject("ad-name", 
                          "ad-id", 
                          1L, 
                          15D);
   HashMap<String, String> adMetadata = 
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   adMetadata.put(MediaConstants.AdMetadataKeys.ADVERTISER, 
                  "Sample Advertiser");
   adMetadata.put(MediaConstants.AdMetadataKeys.CAMPAIGN_ID, 
                  "Sample Campaign");
   
   // Custom metadata keys
   adMetadata.put("affiliate", 
                  "Sample affiliate");
   _tracker.trackEvent(Media.Event.AdStart, 
                       adObject, 
                       adMetadata);
   ```
