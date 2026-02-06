---
title: Scopri come effettuare la migrazione da Milestone a Media Analytics
description: Scopri come modificare le variabili Milestone nelle metriche di Media Analytics e i metodi del modulo Milestone nella sintassi di Media Analytics.
uuid: fdc96146-af63-48ce-b938-c0ca70729277
exl-id: 655841ed-3a02-4e33-bbc9-46fb14302194
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 100%

---

# Migrazione da Milestone a Media Analytics {#migrating-from-milestone-to-media-analytics}

## Panoramica {#overview}

I concetti di base della misurazione video sono gli stessi per Milestone e Media Analytics, ovvero l’acquisizione degli eventi del lettore video e la relativa mappatura sui metodi di Analytics, nonché l’acquisizione dei metadati e dei valori del lettore e la relativa mappatura sulle variabili di Analytics. La soluzione Media Analytics è stata sviluppata da Milestone, quindi anche se molti dei metodi e delle metriche sono gli stessi, l’approccio di configurazione e il codice sono cambiati in modo significativo. Dovrebbe essere possibile aggiornare il codice evento del lettore per indicare i nuovi metodi di Media Analytics. Per maggiori informazioni sull’implementazione di Media Analytics, consulta [Panoramica di SDK](/help/legacy/setup/legacy-setup-overview.md) e [Panoramica del tracciamento](/help/use-cases/track-av-playback/track-core-overview.md).

Le tabelle seguenti forniscono traduzioni tra la soluzione Milestone e Media Analytics.

## Guida alla migrazione {#migration-guide}

### Riferimento variabile

| Metrica Milestone | Tipo di variabile | Metrica di Media Analytics |
| --- | --- | --- |
| Contenuto | Scadenza predefinita eVar <br>: visita | Contenuto |
| Tipo di contenuto | Scadenza predefinita eVar <br>: visualizzazione pagina | Tipo di contenuto |
| Tempo trascorso dei contenuti | Tipo di <br>evento: contatore | Tempo trascorso dei contenuti |
| Inizia video | Tipo di <br>evento: contatore | Inizia video |
| Completamento video | Tipo di <br>evento: contatore | Completamento contenuto |


### Variabili del modulo multimediale

| Milestone | Sintassi di Milestone | Media Analytics | Sintassi di Media Analytics |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | N/D | Tutti i dati di Media Analytics vengono inviati solamente utilizzando i dati contestuali. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N/D | I dati contestuali di Media Analytics vengono popolati automaticamente in variabili riservate. Mappatura per eVar, prop ed eventi non più necessari all’interno del codice di implementazione. I clienti possono mappare i dati contestuali per le variabili utilizzando le regole di elaborazione. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | N/D | Non è più necessario in quanto la mappatura avviene tramite variabili riservate e regole di elaborazione. |
| media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | N/D | Non è più necessario in quanto la mappatura avviene tramite variabili riservate e regole di elaborazione. |

### Variabili facoltative

| Milestone | Sintassi di Milestone | Media Analytics | Sintassi di Media Analytics |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N/D | Le mappature del lettore predefinite non sono più fornite. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N/D | Le mappature del lettore predefinite non sono più fornite. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N/D | Il completamento del contenuto supporta solo un indicatore di avanzamento al 100%. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N/D | Il completamento del contenuto supporta solo un indicatore di avanzamento al 100%. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Chiave SDK: playerName;<br> Chiave API: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N/D | Media Analytics è impostato su 10 secondi per il contenuto e su 1 secondo per gli annunci. Non sono disponibili altre opzioni. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N/D | Media Analytics tiene sempre traccia degli indicatori di avanzamento al 10%, 25%, 50%, 75%, 95%. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Media Analytics tiene sempre traccia degli indicatori di avanzamento al 10%, 25%, 50%, 75%, 95%. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N/D | Il tracciamento automatico non è più disponibile. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N/D | Il tracciamento automatico non è più disponibile. |

### Variabili di tracciamento degli annunci

| Milestone | Sintassi di Milestone | Media Analytics | Sintassi di Media Analytics |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N/D | Media Analytics è impostato su 10 secondi per il contenuto e su 1 secondo per gli annunci. Non sono disponibili altre opzioni. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N/D | Per impostazione predefinita, gli indicatori di avanzamento non sono disponibili per gli annunci. Utilizza le metriche calcolate per creare gli indicatori di avanzamento degli annunci. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Media Analytics è impostato a 1 secondo per gli annunci. Non sono disponibili altre opzioni. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N/D | Il tracciamento automatico non è più disponibile. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N/D | Il tracciamento automatico non è più disponibile. |

### Metodi del modulo multimediale

| Milestone | Sintassi di Milestone | Media Analytics | Sintassi di Media Analytics |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName | `mediaName`: (obbligatorio) il nome del video come desideri che venga visualizzato nei rapporti video. | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength | `mediaLength`: (obbligatorio) la durata del video in secondi. | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName | `mediaPlayerName`: (obbligatorio) il nome del lettore multimediale utilizzato per visualizzare il video, come desideri che venga visualizzato nei rapporti video. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name | `name`: (obbligatorio) il nome o l’ID dell’annuncio. | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length | `length`: (obbligatorio) la durata dell’annuncio. | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName | `playerName`: (obbligatorio) il nome del lettore multimediale utilizzato per visualizzare l’annuncio. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName | `parentName`: il nome o l’ID del contenuto principale in cui l’annuncio è incorporato. | N/D | Ereditato automaticamente. |
| parentPod | `parentPod`: la posizione nel contenuto principale in cui è stato riprodotto l’annuncio. | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition | `parentPodPosition`: la posizione all’interno del pod in cui viene riprodotto l’annuncio. | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM | `CPM`: il CPM o il CPM crittografato (con prefisso “~”) che si applica a questa riproduzione. | N/D | Non disponibile per impostazione predefinita in Media Analytics. |
| Media.click | `s.Media.click(name, offset)` | N/D | Utilizza una chiamata Analytics del collegamento personalizzato per tenere traccia dei clic. |
| Media.close | `s.Media.close(mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(name, offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(mediaName, mediaOffset)` | trackPause <br> o <br> trackEvent | `trackPause()` <br> o `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> o <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | Utilizza metadati personalizzati o standard per impostare variabili aggiuntive. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(mediaName)` | N/D | La frequenza della chiamata del tracciamento viene impostata automaticamente. |
