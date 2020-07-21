---
title: Migrazione da Milestone a Media  Analytics
description: null
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: tm+mt
source-git-commit: aa2a230daa96b823f9963345ac4578799e59d3f5
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 12%

---


# Migrazione da Milestone a Media  Analytics {#migrating-from-milestone-to-media-analytics}

## Panoramica {#overview}

I concetti di base della misurazione video sono gli stessi per Milestone e Media  Analytics, che sta prendendo gli eventi del lettore video e li mappando ai metodi di analisi, acquisite anche i metadati e i valori del lettore e li mappano alle variabili di analisi. La soluzione Media  Analytics è nata da Milestone, quindi molti dei metodi e delle metriche sono gli stessi, tuttavia, l&#39;approccio di configurazione e il codice sono cambiati in modo significativo. Dovrebbe essere possibile aggiornare il codice evento del lettore per puntare ai nuovi metodi Media  Analytics. Per ulteriori informazioni sull’implementazione di Media  Analytics, consulta Panoramica [](/help/sdk-implement/setup/setup-overview.md) SDK e Panoramica [sul](/help/sdk-implement/track-av-playback/track-core-overview.md) tracciamento.

Le tabelle seguenti contengono le traduzioni tra la soluzione Milestone e la soluzione Media  Analytics.

## Migration guide {#migration-guide}

### Riferimento variabile

| Metrica cardine | Tipo di variabile | Media  Analytics Metric |
| --- | --- | --- |
| Contenuto | Scadenza<br>eVarDefault: Visita | Contenuto |
| Tipo di contenuto | eVar<br> Default expiration: Page view | Tipo di contenuto |
| Tempo contenuto trascorso | Tipo evento<br> : Contatore | Tempo contenuto trascorso |
| Avvio video | Tipo evento<br> : Contatore | Avvio video |
| Completamento video | Tipo evento<br> : Contatore | Content Complete |

### Variabili del modulo multimediale

| Milestone | Sintassi pietra miliare | Media Analytics | Sintassi Analytics  Media |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | N/D | Tutti i dati multimediali  Analytics vengono inviati solo utilizzando i dati contestuali. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N/D | I dati contestuali di Analytics  Media vengono automaticamente inseriti in variabili riservate. Mappatura a eVar, prop ed eventi non più necessari all&#39;interno del codice di implementazione. I clienti possono mappare i dati contestuali alle variabili utilizzando le regole di elaborazione. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | N/D | Non è più necessario in quanto la mappatura avviene tramite variabili riservate e regole di elaborazione. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | N/D | Non è più necessario in quanto la mappatura avviene tramite variabili riservate e regole di elaborazione. |

### Variabili facoltative

| Milestone | Sintassi pietra miliare | Media Analytics | Sintassi Analytics  Media |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N/D | Non vengono più fornite mappature di lettore preconfigurate. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N/D | Non vengono più fornite mappature di lettore preconfigurate. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N/D | Content Complete (Completo contenuto) supporta solo un indicatore di avanzamento del 100%. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N/D | Content Complete (Completo contenuto) supporta solo un indicatore di avanzamento del 100%. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Chiave SDK: playerName;<br> Chiave API: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N/D | Media  Analytics è impostato su 10 secondi per i contenuti e su 1 secondo per gli annunci. Non sono disponibili altre opzioni. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N/D | Media  Analytics tiene sempre traccia dei marcatori di avanzamento a 10%, 25%, 50%, 75%, 95% |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Media  Analytics tiene sempre traccia dei marcatori di avanzamento a 10%, 25%, 50%, 75%, 95% |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N/D | La traccia automatica non è più disponibile. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N/D | La traccia automatica non è più disponibile. |

### Variabili di tracciamento annunci

| Milestone | Sintassi pietra miliare | Media Analytics | Sintassi Analytics  Media |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N/D | Media  Analytics è impostato su 10 secondi per i contenuti e su 1 secondo per gli annunci. Non sono disponibili altre opzioni. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N/D | Gli indicatori di avanzamento non sono forniti per impostazione predefinita per gli annunci. Utilizza le metriche calcolate per creare indicatori di avanzamento e avanzamento. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Per gli annunci  Media Analytics è impostato su 1 secondo. Non sono disponibili altre opzioni. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N/D | La traccia automatica non è più disponibile. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N/D | La traccia automatica non è più disponibile. |

### Metodi del modulo multimediale

| Milestone | Sintassi pietra miliare | Media Analytics | Sintassi Analytics  Media |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName - (Obbligatorio) <br> Il nome del video come desiderate venga visualizzato nei rapporti video. | `mediaName` | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength - (Obbligatorio) <br> La lunghezza del video in secondi. | `mediaLength` | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName - (Obbligatorio) <br> Il nome del lettore multimediale utilizzato per visualizzare il video, così come si desidera venga visualizzato nei rapporti video. | `mediaPlayerName` | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name - (Obbligatorio) <br> Il nome o l&#39;ID dell&#39;annuncio. | `name` | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length - (Obbligatorio) <br> La lunghezza dell&#39;annuncio. | `length` | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName - (Obbligatorio) <br> Il nome del lettore multimediale utilizzato per visualizzare l&#39;annuncio. | `playerName` | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName <br> Il nome o l&#39;ID del contenuto principale in cui l&#39;annuncio è incorporato. | `parentName` | N/D | ereditato automaticamente |
| parentPod <br> La posizione nel contenuto principale in cui è stato riprodotto l&#39;annuncio. | `parentPod` | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition <br> La posizione all&#39;interno del contenitore in cui viene riprodotto l&#39;annuncio. | `parentPodPosition` | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM <br> Il CPM o CPM crittografato (con il prefisso &quot;~&quot;) che si applica a questa riproduzione. | `CPM` | N/D | Per impostazione predefinita, non è disponibile in Media  Analytics. |
| Media.click | `s.Media.click(` <br> `  name,` <br> `  offset)` | N/D | Utilizza una chiamata di analisi dei collegamenti personalizzata per tenere traccia dei clic. |
| Media.close | `s.Media.close(` <br> `  mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | trackPause <br> o <br> trackEvent | `trackPause()` <br> o `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> o <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | Utilizzate metadati personalizzati o standard per impostare ulteriori variabili. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | N/D | La frequenza delle chiamate di tracciamento viene impostata automaticamente. |

