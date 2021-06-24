---
title: '"Migrazione dall’SDK per contenuti multimediali indipendenti ad Adobe Launch - Android"'
description: Scopri come migrare da Media SDK a Launch per Android.
exl-id: 26764835-4781-417b-a6c0-ea6ae78d76ae
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# Migrazione dall’SDK di Media autonomo ad Adobe Launch - Android

## Configurazione

### SDK per contenuti multimediali indipendenti

Nell’SDK di Media autonomo, configuri il tracciamento nell’app e lo trasmetti a
SDK quando crei il tracker.

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

### Estensione Launch

1. In Experience Platform Launch, fai clic sulla scheda [!UICONTROL Extensions] per
proprietà mobile.
1. Nella scheda [!UICONTROL Catalog] , individua gli Adobi Medium Analytics for Audio .
e estensione Video, quindi fai clic su [!UICONTROL Install].
1. Nella pagina delle impostazioni dell&#39;estensione, configura i parametri di tracciamento.
L’estensione Media utilizza i parametri configurati per il tracciamento.

![](assets/launch_config_mobile.png)

[Utilizzo di estensioni mobili](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

## Creazione del tracciamento

### SDK per contenuti multimediali indipendenti

Nell’SDK di Media autonomo puoi creare manualmente l’oggetto `MediaHeartbeatConfig`
e configura i parametri di tracciamento. Implementare l’interfaccia delegate che espone
`getQoSObject()` e `getCurrentPlaybackTime()functions.`
Crea un&#39;istanza `MediaHeartbeat` per il tracciamento.

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

### Estensione Launch

[Riferimento API Media - Creare un tracciamento Media](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

Prima di creare il tracker, è necessario registrare l&#39;estensione media e
estensioni dipendenti dal core mobile.

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

Una volta registrata l&#39;estensione media, crea il tracker utilizzando la seguente API.
Il tracker seleziona automaticamente la configurazione dalla proprietà di avvio configurata.

```java
Media.createTracker(new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker tracker) {
        // Use the instance for tracking media.
    }
});
```

## Aggiornamento della testina di riproduzione e dei valori di qualità dell’esperienza.

### SDK per contenuti multimediali indipendenti

Nell’SDK di Media autonomo, trasmetti un oggetto delegato che implementa il
Interfaccia `MediaHeartbeartDelegate` durante la creazione del tracker.  Implementazione
deve restituire l&#39;ultimo QoE e playhead ogni volta che il tracker chiama il
Metodi di interfaccia `getQoSObject()` e `getCurrentPlaybackTime()` .

### Estensione Launch

L&#39;implementazione deve aggiornare l&#39;attuale playhead del lettore chiamando il
Metodo `updateCurrentPlayhead` esposto dal tracker. Tracciamento accurato
dovresti chiamare questo metodo almeno una volta al secondo.

[Riferimento API per i contenuti multimediali - Aggiorna il lettore corrente](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

L&#39;implementazione deve aggiornare le informazioni QoE chiamando `updateQoEObject`
metodo esposto dal tracker. Ci aspettiamo che questo metodo venga chiamato ogni volta che ci sono
è un cambiamento nelle metriche di qualità.

[Riferimento API Media - Aggiorna oggetto QoE](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

## Trasmissione dei contenuti multimediali e dei metadati standard di annunci

### SDK per contenuti multimediali indipendenti

* Metadati contenuti multimediali standard:

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

### Estensione Launch

* Metadati contenuti multimediali standard:

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
