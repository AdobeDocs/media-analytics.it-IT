---
title: Migrazione da Media SDK standalone ad Adobe Launch - Android
description: Scopri come migrare da Media SDK a Launch per Android.
exl-id: 26764835-4781-417b-a6c0-ea6ae78d76ae
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/HawnzTGV1nsGCibAtXkl3cAB5NjO2VfUpQODm6-w-qk
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 425
ht-degree: 48%

---

# Migrazione da Media SDK standalone ad Adobe Launch - Android

>[!NOTE]
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=it) come riferimento consolidato delle modifiche terminologiche.


## Configurazione

### SDK per contenuti multimediali indipendenti

In Media SDK standalone, configura il tracciamento nell’app e trasmettilo a
SDK quando crei il tracciatore.

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

1. In Experience Platform Launch, fai clic sulla scheda [!UICONTROL Extensions] per il
proprietà mobile.
1. Nella scheda [!UICONTROL Catalog], individua Adobe Media Analytics for Audio
e Video e fare clic su [!UICONTROL Install].
1. Nella pagina delle impostazioni dell’estensione, configura i parametri di tracciamento.
L’estensione Media utilizza i parametri configurati per il tracciamento.

![](assets/launch_config_mobile.png)

[Utilizzo delle estensioni per dispositivi mobili](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

## Creazione del tracciamento

### SDK per contenuti multimediali indipendenti

In Media SDK standalone si crea manualmente l&#39;oggetto `MediaHeartbeatConfig`
e configura i parametri di tracciamento. Implementare l’interfaccia delegata che espone
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

[Guida di riferimento dell’API Media: creare un tracciatore Media](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createtracker)

Prima di creare il tracciatore, è necessario registrare l’estensione multimediale e
estensioni dipendenti con il core mobile.

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

Una volta registrata l’estensione Media, crea il tracciatore utilizzando la seguente API.
Il tracciatore seleziona automaticamente la configurazione dalla proprietà di avvio configurata.

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

In Media SDK standalone, trasmetti un oggetto delegato che implementa
Interfaccia `MediaHeartbeartDelegate` durante la creazione del tracker.  Implementazione
deve restituire il QoE e la testina di riproduzione più recente ogni volta che il tracciatore chiama
Metodi dell&#39;interfaccia `getQoSObject()` e `getCurrentPlaybackTime()`.

### Estensione Launch

L’implementazione deve aggiornare la testina di riproduzione corrente del lettore chiamando il
Metodo `updateCurrentPlayhead` esposto dal tracker. Per un tracciamento accurato
è necessario chiamare questo metodo almeno una volta al secondo.

[Guida di riferimento dell’API Media: aggiornare il lettore corrente](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#updatecurrentplayhead)

L’implementazione deve aggiornare le informazioni QoE chiamando il `updateQoEObject`
metodo esposto dal tracker. Ci aspettiamo che questo metodo venga chiamato ogni volta che ci
è una modifica nelle metriche di qualità.

[Guida di riferimento dell’API Media: aggiornare l’oggetto QoE](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createqoeobject)

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
