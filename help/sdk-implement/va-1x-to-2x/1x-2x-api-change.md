---
title: Conversione API da 1.x a 2.x
description: Esplora i riferimenti e gli elenchi delle API di tracciamento richieste e facoltative per le versioni 1.x e 2.x dell’SDK di Media.
uuid: 6e619288-c082-4cb4-8685-e90823dadf4a
exl-id: 8d06b7df-f246-49e6-aa58-91a9d6fa889a
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 5%

---

# Conversione da API 1.x a 2.x {#one-x-to-two-x-conv}

## Riferimenti API Media SDK 2.x

* [Riferimento API per Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/index.html)
* [Riferimento API per iOS](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/index.html)
* [Riferimento API JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html)
* [Riferimento API per Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/index.html)

## API Track* richieste:

|  VHL 1.x  | VHL 2.x |
|---|---|
| `videoPlayerPlugin.trackVideoLoad()` | N/D |
| `videoPlayerPlugin.trackSessionStart()` | [mediaHeartbeat.trackSessionStart(mediaObject, mediaCustomMetadata)](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionStart) |
| `videoPlayerPlugin.trackPlay()` | [mediaHeartbeat.trackPlay()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPlay) |
| `videoPlayerPlugin.trackPause()` | [mediaHeartbeat.trackPause()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPause) |
| `videoPlayerPlugin.trackComplete()` | [mediaHeartbeat.trackComplete()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackComplete) |
| `videoPlayerPlugin.trackVideoUnload()` | [mediaHeartbeat.trackSessionEnd()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionEnd) |
| `videoPlayerPlugin.trackApplicationError()` | N/D |
| `videoPlayerPlugin.trackVideoPlayerError()` | [mediaHeartbeat.trackError()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackError) |

Tutte le API di tracciamento facoltative, come (Annunci, Capitoli, Modifica bitrate, Ricerca e Buffering) ora fanno parte di un&#39;unica API `trackEvent`. L&#39;API [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackEvent) riceve un parametro costante che rappresenta il tipo di evento di cui si intende tenere traccia:

## API trackEvent opzionali:

| VHL 1.x | VHL 2.x |
|---|---|
| Restituisce un elemento `AdBreakInfo` valido in `VideoPlayerPlugin.getAdBreakInfo()` | `trackEvent(Event.AdBreakStart)` |
| Restituisce null in `VideoPlayerPlugin.getAdBreakInfo()` | `trackEvent(Event.AdBreakComplete)` |
| `playerPlugin.trackAdStart()` | `trackEvent(Event.AdStart, adObject, adCustomMetadata)` |
| `playerPlugin.trackAdComplete()` | `trackEvent(Event.AdComplete)` |
| Restituisce null in `VideoPlayerPlugin.getAdInfo()` | `trackEvent(Event.AdSkip)` |
| `playerPlugin.trackChapterStart()` | `trackEvent(Event.ChapterStart, chapterObject, chapterCustomMetadata)` |
| `playerPlugin.trackChapterComplete()` | `trackEvent(Event.ChapterComplete)` |
| Restituisce null in `VideoPlayerPlugin.getChapterInfo()` | `trackEvent(Event.ChapterSkip)` |
| `playerPlugin.trackSeekStart()` | `trackEvent(Event.SeekStart)` |
| `playerPlugin.trackSeekComplete()` | `trackEvent(Event.SeekComplete)` |
| `playerPlugin.trackBufferStart()` | `trackEvent(Event.BufferStart)` |
| `playerPlugin.trackBufferComplete()` | `trackEvent(Event.BufferComplete)` |
| `playerPlugin.trackBitrateChange()` | `trackEvent(Event.BitrateChange)` |
| `playerPlugin.trackTimedMetadata()` | `trackEvent(Event.TimedMetadataUpdate)` |
