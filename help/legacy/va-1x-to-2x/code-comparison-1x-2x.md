---
title: Confronto tra codici v1.x e v2.x
description: Scopri la differenza tra il codice nelle versioni 1.x e 2.x di Media SDK.
uuid: 9f0a1660-2100-446d-ab75-afdf966478b3
exl-id: c2324c6a-329f-44e2-bea0-9d43ef9c6ef7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 98%

---

# Confronto tra codici legacy: da 1.x a 2.x {#code-comparison-x-to-x}

Tutti i parametri di configurazione e le API di tracciamento sono ora consolidati nelle classi `MediaHeartbeats` e `MediaHeartbeatConfig`.

**Modifiche all’API di configurazione:**

* `AdobeHeartbeatPluginConfig.sdk` è stato rinominato `MediaConfig.appVersion`
* `MediaHeartbeatConfig.playerName` adesso è impostato tramite `MediaHeartbeatConfig` anziché `VideoPlayerPluginDelegate`
* (Solo per JavaScript): l’istanza `AppMeasurement` adesso è inviata tramite il generatore `MediaHeartbeat`.

**Modifiche alle proprietà di configurazione:**

* `sdk` è stato rinominato `appVersion`
* `publisher` è stato rimosso. L’ID organizzazione di Experience Cloud viene utilizzato come editore
* `quiteMode` è stato rimosso

**Collegamenti ai lettori di esempio 1.x e 2.x:**

* [1.x Lettore di esempio](https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L58)
* [2.x Lettore di esempio](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/2.x/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L47)

Le sezioni seguenti forniscono confronti di codice tra 1.x e 2.x, inclusi l’Inizializzazione, la Riproduzione core, la Riproduzione di annunci, la Riproduzione di capitoli e alcuni eventi aggiuntivi.

## Confronto tra codici VHL: INIZIALIZZAZIONE

### Inizializzazione oggetti

| API 1.x | API 2.x |
| --- | --- |
| `Heartbeat()` | `MediaHeartbeat()` |
| `VideoPlayerPlugin()` | `MediaHeartbeatConfig()` |
| `AdobeAnalyticsPlugin()` | |
| `HeartbeatPlugin()` | |

#### Inizializzazione del plug-in del lettore video (1.x) {#plugin-init-1.x}

```js
this._playerPlugin = new VideoPlayerPlugin( new SampleVideoPlayerPluginDelegate(this._player));
var playerPluginConfig = new VideoPlayerPluginConfig();
playerPluginConfig.debugLogging = true;

// Set up the AppMeasurement plugin
this._aaPlugin = new AdobeAnalyticsPlugin( appMeasurement, new SampleAdobeAnalyticsPluginDelegate());
var aaPluginConfig = new AdobeAnalyticsPluginConfig();
aaPluginConfig.channel = Configuration.HEARTBEAT.CHANNEL;
aaPluginConfig.debuglogging = true;
this._aaPlugin.configure(aaPluginConfig);

// Set up the AdobeHeartbeat plugin
var ahPlugin = new AdobeHeartbeatPlugin( new SampleAdobeHeartbeatPluginDelegate());
var ahPluginConfig = new AdobeHeartbeatPluginConfig( configuration.HEARTBEAT.TRACKING_SERVER, configuration.HEARTBEAT.PUBLISHER);
ahPluginConfig.ovp = configuration.HEARTBEAT.OVP;
ahPluginConfig.sdk = configuration.HEARTBEAT.SDK;
ahPluginConfig.debugLogging = true;
ahPlugin.configure(ahPluginConfig);
var plugins = [this._playerPlugin, this._aaPlugin, ahPlugin];

// Set up and configure the heartbeat library this._heartbeat = new Heartbeat(new SampleHeartbeatDelegate(), plugins);
var configData = new HeartbeatConfig();
configData.debugLogging = true;
this._heartbeat.configure(configData);
```

#### Inizializzazione Media Heartbeat (2.x) {#mh-init-2.x}

```js
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
mediaConfig.playerName = Configuration.PLAYER.NAME;
mediaConfig.debugLogging = true;
mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL;
mediaConfig.ssl = false;
mediaConfig.ovp = Configuration.HEARTBEAT.OVP;
mediaConfig.appVersion = Configuration.HEARTBEAT.SDK;
this._mediaHeartbeat = new MediaHeartbeat( new SampleMediaHeartbeatDelegate(this._player), mediaConfig, appMeasurement);
```

### Delegati

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPluginDelegate()` | `MediaHeartbeatDelegate()` |
| `VideoPlayerPluginDelegate().getVideoInfo` | `MediaHeartbeatDelegate().getCurrentPlaybackTime` |
| `VideoPlayerPluginDelegate().getAdBreakInfo` | `MediaHeartbeatDelegate().getQoSObject` |
| `VideoPlayerPluginDelegate().getAdInfo` | |
| `VideoPlayerPluginDelegate().getChapterInfo` | |
| `VideoPlayerPluginDelegate().getQoSInfo` | |
| `VideoPlayerPluginDelegate().get.onError` | |
| `AdobeAnalyticsPluginDelegate()` | |

#### VideoPlayerPluginDelegate (1.x) {#player-plugin-delegate-1.x}

```js
$.extend(SampleVideoPlayerPluginDelegate.prototype, VideoPlayerPluginDelegate.prototype);

function SampleVideoPlayerPluginDelegate(player) {
    this._player = player;
}

SampleVideoPlayerPluginDelegate.prototype.getVideoInfo = function() {
    return this._player.getVideoInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getAdBreakInfo = function() {
    return this._player.getAdBreakInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() {
    return this._player.getAdInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() {
    return this._player.getChapterInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getQoSInfo = function() {
    return this._player.getQoSInfo();
};
```

#### AdobeAnalyticsPluginDelegate (1.x) {#analytics-plugin-delegate-1.x}

```js
$.extend(SampleAdobeAnalyticsPluginDelegate.prototype, AdobeAnalyticsPluginDelegate.prototype);

function SampleAdobeAnalyticsPluginDelegate() {}

SampleAdobeAnalyticsPluginDelegate.prototype.onError = function(errorInfo) {
    console.log("AdobeAnalyticsPlugin error: " + errorInfo.getMessage() + " | " + errorInfo.getDetails());
};
```

#### HeartbeatDelegate (1.x) {#hb-delegate-1.x}

```js
$.extend(SampleHeartbeatDelegate.prototype, HeartbeatDelegate.prototype);

function SampleHeartbeatDelegate() {}

SampleHeartbeatDelegate.prototype.onError = function(errorInfo) {
    console.log("Heartbeat error: " + errorInfo.getMessage() + " | " + errorInfo.getDetails());
};
```

#### MediaHeartbeatDelegate (2.x) {#mh-delegate-2.x}

```js
ADB.core.extend(SampleMediaHeartbeatDelegate.prototype, MediaHeartbeatDelegate.prototype);

function SampleMediaHeartbeatDelegate(player) {
    this._player = player;
}

SampleMediaHeartbeatDelegate.prototype.getCurrentPlaybackTime = function() {
    return this._player.getCurrentPlaybackTime();
};

SampleMediaHeartbeatDelegate.prototype.getQoSObject = function() {
    return this._player.getQoSInfo();
};

this._mediaHeartbeat = new MediaHeartbeat(new SampleMediaHeartbeatDelegate(this._player), mediaConfig, appMeasurement);
```

## Confronto tra codici VHL: RIPRODUZIONE CORE

### Avvio sessione

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPluginDelegate.trackVideoLoad()` | `MediaHeartbeat.createMediaObject()` |
| `VideoPlayerPluginDelegate.getVideoInfo()` | `MediaHeartbeat.trackSessionStart()` |

#### Avvio sessione (1.x) {#session-start-1.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    this._playerPlugin.trackVideoLoad();
};

SampleVideoPlayerPluginDelegate.prototype.getVideoInfo = function() {
    return this._player.getVideoInfo();
};

VideoPlayer.prototype.getVideoInfo = function() {
    this._videoInfo.playhead = vTime;
    return this._videoInfo;
};
```

#### Avvio sessione (2.x) {#session-start-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    var contextData = {};
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

### Metadati video standard

| API 1.x | API 2.x |
| --- | --- |
| `VideoMetadataKeys()` | `MediaHeartbeat.createMediaObject()` |
| `AdobeAnalyticsPlugin.setVideoMetadata()` | `MediaHeartbeat.trackSessionStart()` |

#### Metadati standard (1.x) {#std-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    console.log('Player event: MEDIA_LOAD');

    var contextData = {};

    // Setting Standard Video Metadata
    contextData[VideoMetadataKeys.SEASON] = "sample season";
    contextData[VideoMetadataKeys.SHOW] = "sample show";
    contextData[VideoMetadataKeys.EPISODE] = "sample episode";
    contextData[VideoMetadataKeys.ASSET_ID] = "sample asset id";
    contextData[VideoMetadataKeys.GENRE] = "sample genre";
    contextData[VideoMetadataKeys.FIRST_AIR_DATE] = "sample air date";

    // Etc.
    this._aaPlugin.setVideoMetadata(contextData);
    this._playerPlugin.trackVideoLoad();
};
```

#### Metadati standard (2.x) {#std-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    console.log('Player event: MEDIA_LOAD');
    var contextData = {};
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);

    // Set standard Video Metadata
    var standardVideoMetadata = {};
    standardVideoMetadata[VideoMetadataKeys.SEASON] = "sample season";
    standardVideoMetadata[VideoMetadataKeys.SHOW] = "sample show";
    standardVideoMetadata[VideoMetadataKeys.EPISODE] = "sample episode";
    standardVideoMetadata[VideoMetadataKeys.ASSET_ID] = "sample asset id";
    standardVideoMetadata[VideoMetadataKeys.GENRE] = "sample genre";
    standardVideoMetadata[VideoMetadataKeys.FIRST_AIR_DATE] = "sample air date";

    // Etc.
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

>[!NOTE]
>Invece di impostare i metadati video standard tramite l’API `AdobeAnalyticsPlugin.setVideoMetadata()` in VHL 2.0, i metadati video standard sono impostati tramite la chiave MediaObject `MediaObject.MediaObjectKey.StandardVideoMetadata()`.

### Metadati video personalizzati

| API 1.x | API 2.x |
| --- | --- |
| `VideoMetadataKeys()` | `MediaHeartbeat.createMediaObject()` |
| `AdobeAnalyticsPlugin.setVideoMetadata()` | `MediaHeartbeat.trackSessionStart()` |

#### Metadati personalizzati (1.x) {#custom-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    var contextData = {
        isUserLoggedIn: "false",
        tvStation: "Sample TV station",
        programmer: "Sample programmer"
    };
    this._aaPlugin.setVideoMetadata(contextData);
    this._playerPlugin.trackVideoLoad();
};
```

#### Metadati personalizzati (2.x) {#custom-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    var contextData = {
        isUserLoggedIn: "false",
        tvStation: "Sample TV station",
        programmer: "Sample programmer"
    };
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

>[!NOTE]
>Invece di impostare i metadati video personalizzati tramite l’API `AdobeAnalyticsPlugin.setVideoMetadata()` in VHL 2.0, i metadati video standard sono impostati tramite l’API `MediaHeartbeat.trackSessionStart()`.


### Riproduzione

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackPlay()` | `MediaHeartbeat.trackPlay()` |

#### Riproduzione (1.x) {#playback-1.x}

```js
VideoAnalyticsProvider.prototype._onSeekStart = function() {
    console.log('Player event: SEEK_START');
    this._playerPlugin.trackSeekStart();
};
```

#### Riproduzione (2.x) {#playback-2.x}

```js
VideoAnalyticsProvider.prototype._onSeekStart = function() {
    console.log('Player event: SEEK_START');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
};
```

### Pausa

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackPause()` | `MediaHeartbeat.trackPausel()` |

#### Pausa (1.x) {#pause-1.x}

```js
VideoAnalyticsProvider.prototype._onPause = function() {
    console.log('Player event:X PAUSE');
    this._playerPlugin.trackPause();
};
```

#### Pausa (2.x) {#pause-2.x}

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() {
    console.log('Player event: BUFFER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

### Ricerca completata

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackSeekComplete()` | `MediaHeartbeat.`<br/>  `trackEvent(MediaHeartbeat.Event.SeekComplete)` |

#### Ricerca (1.x) {#seek-1.x}

```js
VideoAnalyticsProvider.prototype._onSeekComplete = function() {
    console.log('Player event: SEEK_COMPLETE');
    this._playerPlugin.trackSeekComplete();
};
```

#### Ricerca (2.x) {#seek-2.x}

```js
VideoAnalyticsProvider.prototype._onSeekComplete = function() {
    console.log('Player event: SEEK_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
};
```

### Avvio buffer

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackBufferStart()` | `MediaHeartbeat.trackEvent(`<br/>  `MediaHeartbeat.Event.BufferStart)` |

#### Avvio buffer (1.x) {#buffer-start-1.x}

```js
VideoAnalyticsProvider.prototype._onBufferStart = function() {
    console.log('Player event: BUFFER_START');
    this._playerPlugin.trackBufferStart();
};
```

#### Avvio buffer (2.x) {#buffer-start-2.x}

```js
VideoAnalyticsProvider.prototype._onBufferStart = function() {
    console.log('Player event: BUFFER_START');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
};
```

### Buffer completo

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackBufferComplete()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.BufferComplete)` |

#### Buffer completo (1.x) {#buffer-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() {
    console.log('Player event: BUFFER_COMPLETE');
    this._playerPlugin.trackBufferComplete();
};
```

#### Buffer completo (2.x) {#buffer-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() {
    console.log('Player event: BUFFER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

### Riproduzione completata

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackComplete()` | `MediaHeartbeat.trackComplete()` |

#### Riproduzione completata (1.x) {#playback-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onComplete = function() {
    console.log('Player event: COMPLETE');
    this._playerPlugin.trackComplete(function() {
        console.log( "The completion of the content has been tracked.");
    });
};
```

#### Riproduzione completata (2.x) {#playback-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onComplete = function() {
    console.log('Player event: COMPLETE');
    this._mediaHeartbeat.trackComplete();
};
```

## Confronto tra codici VHL: RIPRODUZIONE ANNUNCIO

### Avvio annuncio

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackAdStart()` | `MediaHeartbeat.createAdBreakObject()` |
| `VideoPlayerPluginDelegate.getAdBreakInfo()` | `MediaHeartbeat.createAdObject()` |
| `VideoPlayerPluginDelegate.getAdInfo()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdBreakStart)` |
| | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdStart)` |

#### Avvio annuncio (1.x) {#ad-start-1.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() {
    console.log('Player event: AD_START');
    this._playerPlugin.trackAdStart();
};
```

```js
SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() {
    return this._player.getAdInfo();
};
```

#### Avvio annuncio (2.x) {#ad-start-2.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() {
    console.log('Player event: AD_START');
    var adContextData = {};

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

### Metadati annuncio standard

| API 1.x | API 2.x |
| --- | --- |
| `AdMetadataKeys()` | `MediaHeartbeat.createAdObject()` |
| `AdobeAnalyticsPlugin.setAdMetadata()` | `MediaHeartbeat.trackAdStart()` |

#### Metadati annuncio standard (1.x) {#ad-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() {
    console.log('Player event: AD_START');
    var contextData = {};

    // setting Standard Ad Metadata
    contextData[AdMetadataKeys.ADVERTISER] = "sample advertiser";
    contextData[AdMetadataKeys.CAMPAIGN_ID] = "sample campaign";
    contextData[AdMetadataKeys.CREATIVE_ID] = "sample creative";
    contextData[AdMetadataKeys.CREATIVE_URL] = "sample url";
    contextData[AdMetadataKeys.SITE_ID] = "sample site";
    contextData[AdMetadataKeys.PLACEMENT_ID] = "sample placement";
    this._aaPlugin.setAdMetadata(contextData);
    this._playerPlugin.trackAdStart();
};
```

#### Metadati annuncio standard (2.x) {#ad-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() {
    console.log('Player event: AD_START');
    var adContextData = { };

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);

    // Set standard Ad Metadata
    var standardAdMetadata = {};
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
    adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

>[!NOTE]
>Invece di impostare i metadati standard dell’annuncio tramite l’API `AdobeAnalyticsPlugin.setVideoMetadata()` in VHL 2.0, i metadati dell’annuncio standard sono impostati tramite `AdMetadata` chiave `MediaObject.MediaObjectKey.StandardVideoMetadata`

### Metadati annuncio personalizzati

| API 1.x | API 2.x |
| --- | --- |
| `AdobeAnalyticsPlugin.setAdMetadata()` | `MediaHeartbeat.createAdObject()` |
| | `MediaHeartbeat.trackAdStart()` |

#### Metadati annuncio personalizzati (1.x) {#custom-ad-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() {
    console.log('Player event: AD_START');
    var contextData = {};

    // Setting Standard Ad Metadata
    contextData[AdMetadataKeys.ADVERTISER] = "sample advertiser";
    contextData[AdMetadataKeys.CAMPAIGN_ID] = "sample campaign";
    contextData[AdMetadataKeys.CREATIVE_ID] = "sample creative";
    contextData[AdMetadataKeys.CREATIVE_URL] = "sample url";
    contextData[AdMetadataKeys.SITE_ID] = "sample site";
    contextData[AdMetadataKeys.PLACEMENT_ID] = "sample placement";
    this._aaPlugin.setAdMetadata(contextData);
    this._playerPlugin.trackAdStart();
};
```

#### Metadati annuncio personalizzati (2.x) {#custom-ad-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() {
    console.log('Player event: AD_START');
    var adContextData = {
        affiliate: "Sample affiliate",
        campaign: "Sample ad campaign"
    };

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

>[!NOTE]
>Invece di impostare i metadati dell’annuncio personalizzato tramite l’API `AdobeAnalyticsPlugin.setVideoMetadata` in VHL 2.0, i metadati dell’annuncio standard sono impostati tramite l’API `MediaHeartbeat.trackAdStart()`.

### Salta annuncio

| API 1.x | API 2.x |
| --- | --- |
| `AdobeAnalyticsPlugin.setAdMetadata()` | `MediaHeartbeat.createAdObject()` |
| | `MediaHeartbeat.trackAdStart()` |

#### Salta annuncio (1.x) {#ad-skip-1.x}

```js
SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() {
    return this._player.getAdInfo();
};
```

#### Salta annuncio (2.x) {#ad-skip-2.x}

```js
VideoAnalyticsProvider.prototype._onAdSkip = function() {
    console.log('Player event: AD_SKIP');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
};
```

>[!NOTE]
>Nelle API VHL 1.5.X, `getAdinfo()` e `getAdBreakInfo()` devono restituire null se il lettore si trova al di fuori dei limiti di interruzione dell’annuncio.

### Annuncio completato

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackAdComplete()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdComplete)` |
| | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdBreakComplete)` |

#### Annuncio completato (1.x) {#ad-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onAdComplete = function() {
    console.log('Player event: AD_COMPLETE');
    this._playerPlugin.trackAdComplete();
};
```

#### Annuncio completato (2.x) {#ad-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onAdComplete = function() {
    console.log('Player event: AD_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
};
```

## Confronto tra codici VHL: RIPRODUZIONE CAPITOLO

### Inizio capitolo

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPluginDelegate.getChapterInfo()` | `MediaHeartbeat.createChapterObject` |
| `VideoPlayerPlugin.trackChapterStart()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.ChapterStart)` |

#### Inizio capitolo (1.x) {#chap-start-1.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() {
    console.log('Player event: CHAPTER_START');
    this._playerPlugin.trackChapterStart();
};
```

```js
SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() {
    return this._player.getChapterInfo();
};
```

#### Inizio capitolo (2.x) {#chap-start-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() {
    console.log('Player event: CHAPTER_START');
    var chapterContextData = { };

    // Chapter Info - getting the chapterInfo from player and creating ChapterInfo Object from MediaHeartbeat
    var _chapterInfo = this._player.getChapterInfo();
    var chapterInfo = MediaHeartbeat.createChapterObject(_chapterInfo.name, _chapterInfo.position, _chapterInfo.length, _chapterInfo.startTime);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, chapterInfo, chapterContextData);
};
```

### Salta capitolo

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPluginDelegate.getChapterInfo()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.ChapterSkip)` |

#### Salta capitolo (1.x) {#chap-skip-1.x}

```js
SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() {
    return this._player.getChapterInfo();
};
```

>[!NOTE]
>Nelle API VHL 1.5.X, `getChapterinfo()` deve restituire null se il lettore si trova al di fuori dei limiti del capitolo.

#### Salta capitolo (2.x) {#chap-skip-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterSkip = function() {
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip);
};
```

### Metadati personalizzati del capitolo

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackChapterStart()` | `MediaHeartbeat.createChapterObject()` |
| `AdobeAnalyticsPlugin.setChapterMetadata()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.ChapterStart)` |

#### Metadati personalizzati del capitolo (1.x) {#chap-cust-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() {
    console.log('Player event: CHAPTER_START');
    this._aaPlugin.setChapterMetadata({
        segmentType: "Sample segment type"
    });
    this._playerPlugin.trackChapterStart();
};
```

#### Metadati personalizzati del capitolo (2.x) {#chap-cust-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() {
    console.log('Player event: CHAPTER_START');
    var chapterContextData = {
        segmentType: "Sample segment type"
    };

    // Chapter Info - getting the chapterInfo from player and creating ChapterInfo Object from MediaHeartbeat
    var _chapterInfo = this._player.getChapterInfo();
    var chapterInfo = MediaHeartbeat.createChapterObject(_chapterInfo.name, _chapterInfo.position, _chapterInfo.length, _chapterInfo.startTime);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, chapterInfo, chapterContextData);
};
```

### Capitolo completato

| API 1.x | API 2.x |
| --- | --- |
| `trackChapterComplete()` | `trackEvent(MediaHeartbeat.Event.ChapterComplete)` |

#### Capitolo completato (1.x) {#chap-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onChapterComplete = function() {
    console.log('Player event: CHAPTER_COMPLETE');
    this._playerPlugin.trackChapterComplete();
};
```

#### Capitolo completato (2.x) {#chap-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterComplete = function() {
    console.log('Player event: CHAPTER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete);
};
```

## Confronto tra codici VHL: ALTRI EVENTI

### Modifica bitrate

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackBitrateChange()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.BitrateChange)` |

#### Modifica bitrate (1.x) {#bitrate-chg-1.x}

```js
VideoAnalyticsProvider.prototype._onBitrateChange = function() {
    console.log('Player event: BITRATE_CHANGE');

    // Update getQosInfo to return the updated bitrate
    this._playerPlugin.trackBitrateChange();
};
```

#### Modifica bitrate (2.x) {#bitrate-chg-2.x}

```js
VideoAnalyticsProvider.prototype._onBitrateChange = function() {
    console.log('Player event: BITRATE_CHANGE');

    // Update getQosObject to return the updated bitrate
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange);
};
```

### Riprendi video

| API 1.x | API 2.x |
| --- | --- |
| `VideoInfo.resumed()` | `MediaObject()` |
| `VideoPlayerPluginDelegate.getVideoInfo()` | `MediaHeartbeat.trackSessionStart()` |
| `VideoPlayerPlugin.trackVideoLoad()` | |

#### Riprendi video (1.x) {#video-resume-1.x}

```js
this._videoInfo.resumed=true;
```

```js
VideoPlayer.prototype.getVideoInfo = function() {
    this._videoInfo.playhead = vTime;
    return this._videoInfo;
};
```

#### Riprendi video (2.x) {#video-resume-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    console.log('Player event: MEDIA_LOAD');
    var contextData = {};
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.playerName, videoInfo.id, videoInfo.length, videoInfo.streamType);
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.VideoResumed, true);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

Per ulteriori informazioni sul tracciamento dei video con 2.x, consulta la sezione [Tracciare la riproduzione di video di base.](/help/use-cases/track-av-playback/track-core-overview.md)
