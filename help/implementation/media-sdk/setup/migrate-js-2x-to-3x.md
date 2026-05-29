---
title: Migrazione da JavaScript SDK 2.x a 3.x
description: Guida al confronto dei codici e alla migrazione per l’aggiornamento da Media SDK JavaScript 2.x a SDK 3.x.
feature: Streaming Media
role: User, Admin, Developer
exl-id: b7e2d5a1-8c3f-4a9d-b6e7-2c1b4f0d8a3e
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 12%

---


# Migrazione da SDK JS 2.x a SDK JS 3.x

## Nuove funzionalità

* Utilizzare le API MediaCollection
* Tracciamento dello stato personalizzato

## Miglioramenti

* Fornisci configurazione globale per libreria multimediale
* Creazione di un tracker semplice
* API aggiunte per fornire informazioni sulla testina di riproduzione e sul QoE
* API per eliminare l’istanza di tracciamento
* Impostazione semplificata di metadati standard/personalizzati per contenuti multimediali e annunci

## Confronto API

### Classe media

| Funzionalità | 2.x | 3.x |
| ------ | ------ | ------ |
| **Spazio dei nomi** | `ADB.va.MediaHeartbeat` | **`ADB.Media`** |
| **Configurazione** | Parametro del costruttore `MediaHeartbeat` | **`configure(mediaConfig, appMeasurement)`** |
| **Crea tracker** | `new MediaHeartbeat(...)` | **`getInstance()`** |
| **Metodi statici** | |  |
|  | `createMediaObject(...)` | `createMediaObject(...)` |
|  | `createAdBreakObject(...)` | `createAdBreakObject(...)` |
|  | `createAdObject(...)` | `createAdObject(...)` |
|  | `createChapterObject(...)` | `createChapterObject(...)` |
|  | `createQoSObject(...)` | **`createQoEObject(...)`** |
|  | N/D | **`createStateObject()`** |
| **Metodi dell&#39;istanza** | |  |
|  | `trackSessionStart(...)` | `trackSessionStart(...)` |
|  | `trackPlay()` | `trackPlay()` |
|  | `trackPause()` | `trackPause()` |
|  | `trackComplete()` | `trackComplete()` |
|  | `trackSessionEnd()` | `trackSessionEnd()` |
|  | `trackEvent(...)` | `trackEvent(...)` |
|  | `trackError(...)` | `trackError(...)` |
|  | N/D | **`updatePlayhead(playhead)`** |
|  | N/D | **`updateQoEObject(qoeObject)`** |
| **Tracciamento distruzione** | N/D | **`destroy()`** |

### Classe MediaConfig

| Funzionalità | 2.x | 3.x |
| ------ | ------ | ------ |
| **Spazio dei nomi** | ` ADB.va.MediaHeartbeatConfig` | **`ADB.MediaConfig`** |
| **Costruttore** | `new MediaHeartbeatConfig()` | **`new MediaConfig()`** |
| **Parametri di configurazione** | | |
| | `trackingServer` | `trackingServer` |
| | `channel` | `channel` |
| | `ovp` | N/D |
| | `appVersion` | `appVersion` |
| | `playerName` | `playerName` |
| | `ssl` | `ssl` |
| | `debugLogging` | `debugLogging` |

## Confronto tra codici

### Creazione di configurazione e tracciamento

#### 2.x

```javascript
    var MediaHeartbeat = ADB.va.MediaHeartbeat;
    var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
    var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;

    // Create MediaHeartbeatConfig object
    var mediaConfig = new MediaHeartbeatConfig();
    mediaConfig.trackingServer = "tracking_server";
    mediaConfig.playerName = "player_name";
    mediaConfig.channel = "sample_channel";
    mediaConfig.ovp = "sample_ovp";
    mediaConfig.appVersion = "app_version";
    mediaConfig.debugLogging = true;
    mediaConfig.ssl = true;

    // Instance of MediaHeartbeatDelegate to return playhead and qosInfo to the tracker
    ADB.core.extend(SampleMediaHeartbeatDelegate.prototype,
                         MediaHeartbeatDelegate.prototype);
    function SampleMediaHeartbeatDelegate() { ... }
    SampleMediaHeartbeatDelegate.prototype.getCurrentPlaybackTime = function() {
        // Returns the current playhead from the player.
    }
    SampleMediaHeartbeatDelegate.prototype.getQoSObject = function() {
        // Returns the current QOS information if available from the player.
    }

    // Create tracker instance by passing mediaConfig, appMeasurement instancee and player delegate
    var tracker = new MediaHeartbeat( new SampleMediaHeartbeatDelegate(),
                                      mediaConfig,
                                      appMeasurement);
```

#### 3.x

```javascript
    var Media = ADB.Media;
    var MediaConfig = ADB.MediaConfig;

    // Create MediaConfig object (same as above)
    var mediaConfig = new MediaConfig();
    mediaConfig.trackingServer = "tracking_server";
    mediaConfig.playerName = "player_name";
    mediaConfig.channel = "sample_channel";
    mediaConfig.appVersion = "app_version";
    mediaConfig.debugLogging = true;
    mediaConfig.ssl = true;

    // Configuration is only done once per page
    // and applies to all tracker instances created.
    Media.configure(mediaConfig, appMeasurement);

    // Tracker creation.
    var tracker = Media.getInstance();
```

### Fornire informazioni sulla testina di riproduzione e sul QoE al tracker

#### 2.x

```javascript
    // Instance of MediaHeartbeatDelegate to return playhead and qosInfo to the tracker
    ADB.core.extend(SampleMediaHeartbeatDelegate.prototype,
                         MediaHeartbeatDelegate.prototype);
    function SampleMediaHeartbeatDelegate(player) { this.player = player }
    SampleMediaHeartbeatDelegate.prototype.getCurrentPlaybackTime = function() {
        // Returns the current playhead from the player.
        return this.player.playhead;
    };
    SampleMediaHeartbeatDelegate.prototype.getQoSObject = function() {
        // Returns the current QOS information if available from the player.
        var qosInfo = MediaHeartbeat.createQoSObject(this._player.bitrate,
                                                     this._player.startupTime,
                                                     this._player.fps,
                                                     this._player.droppedFrames);
        return qosInfo;
    };

    // Pass the delegate instance when creating the tracker.
    var tracker = new MediaHeartbeat( new SampleMediaHeartbeatDelegate(),
                                      mediaConfig,
                                      appMeasurement);
```

#### 3.x

```javascript
        // When playhead changes, call
        tracker.updatePlayhead(this._player.playhead)

        // When new QoE information is available, call
        var qoeInfo = Media.createQoEObject(this._player.bitrate,
                                                     this._player.startupTime,
                                                     this._player.fps,
                                                     this._player.droppedFrames);
        tracker.updateQoEObject(qoeInfo)
```

### Metadati standard e personalizzati per contenuti multimediali e annunci

#### Media

#### 2.x

```javascript
    var mediaObject = MediaHeartbeat.createMediaObject("name",
                                                       "id",
                                                       60.0,
                                                       MediaHeartbeat.StreamType.VOD,
                                                       MediaHeartbeat.MediaType.Video);
    // standard metadata
    var standardMetadata = {};
    standardMetadata[MediaHeartbeat.VideoMetadataKeys.SEASON] = "sample season";
    standardMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "sample show";
    // Set standard metadata on media object.
    mediaObject.setValue(MediaHeartbeat.MediaObjectKey.StandardMediaMetadata,
                               standardMetadata);

    // custom metadata
    var customMetadata = {
        "customKey1" : "custom value",
        "customKey2" : "custom value"
    };

    mediaTracker.trackSessionStart(mediaObject, customMetadata);
```

#### 3.x

```javascript
    var mediaObject = Media.createMediaObject("name",
                                           "id",
                                           60.0,
                                           Media.StreamType.VOD,
                                           Media.MediaType.Video);

    var metadata = {};
    // standard metadata
    metadata[Media.VideoMetadataKeys.Season] = "sample season";
    metadata[Media.VideoMetadataKeys.Show] = "sample show";
    // custom metadata
    metadata["customKey1"] = "custom value";
    metadata["customKey2"] = "custom value";

    mediaTracker.trackSessionStart(mediaObject, metadata);
```

#### Annunci

#### 2.x

```javascript
    var adObject = MediaHeartbeat.createAdObject("adName",
                                                 "adId",
                                                  1,
                                                  15.0);

    // standard metadata
    var standardAdMetadata = {};
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
    // Set standard metadata on ad object.
    adObject.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata,
                               standardAdMetadata);

    // custom metadata
    var customMetadata = {
        "customKey1" : "custom value",
        "customKey2" : "custom value"
    };

    mediaTracker.trackEvent(MediaHeartbeat.Event.AdStart, adObject, customMetadata);
```

#### 3.x

```javascript
    var adObject = Media.createAdObject("adName",
                                                 "adId",
                                                  1,
                                                  15.0);


    var metadata = {};
    // standard metadata
    metadata[Media.AdMetadataKeys.Advertiser] = "Sample Advertiser";
    metadata[Media.AdMetadataKeys.CampaignId] = "Sample Campaign";
    // custom metadata
    metadata["customKey1"] = "custom value";
    metadata["customKey2"] = "custom value";

    mediaTracker.trackEvent(Media.Event.AdStart, adObject, metadata);
```
