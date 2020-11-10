---
title: Migrazione da Milestone ad Media Analytics
description: null
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: tm+mt
source-git-commit: e079b90f8fb9197e5ebae0fb6ca31081ba28de1d
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 14%

---


# Migrazione da Milestone ad Media Analytics {#migrating-from-milestone-to-media-analytics}

## Panoramica {#overview}

I concetti di base della misurazione video sono gli stessi per Milestone e Media Analytics, ovvero prendere gli eventi dei lettori video e mapparli ai metodi di analisi, acquisire anche i metadati e i valori dei lettori e mapparli alle variabili di analisi. La soluzione Media Analytics è nata da Milestone, quindi molti dei metodi e delle metriche sono gli stessi, ma l&#39;approccio di configurazione e il codice sono cambiati in modo significativo. Dovrebbe essere possibile aggiornare il codice evento del lettore per puntare ai nuovi metodi di Media Analytics. Vedere [Panoramica dell&#39;SDK](/help/sdk-implement/setup/setup-overview.md) e [Panoramica di tracciamento](/help/sdk-implement/track-av-playback/track-core-overview.md) per ulteriori dettagli sull’implementazione di Media Analytics.

Le tabelle seguenti contengono le traduzioni tra la soluzione Milestone e la soluzione Media Analytics.

## Guida alla migrazione {#migration-guide}

### Riferimento variabile

| Metrica cardine | Tipo di variabile | Metrica di Media Analytics |
| --- | --- | --- |
| Contenuto |  eVar <br> Scadenza predefinita: Visita | Contenuto |
| Tipo di contenuto |  eVar <br> Scadenza predefinita: Visualizzazione pagina | Tipo di contenuto |
| Tempo contenuto trascorso | Evento <br> Tipo: Contatore | Tempo contenuto trascorso |
| Avvio video | Evento <br> Tipo: Contatore | Avvio video |
| Completamento video | Evento <br> Tipo: Contatore | Content Complete |


### Variabili del modulo multimediale

| Milestone | Sintassi pietra miliare | Media Analytics | Sintassi di Media Analytics |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | N/D | Tutti i dati di Media Analytics vengono inviati solo utilizzando i dati contestuali. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N/D | I dati contestuali di Media Analytics vengono automaticamente inseriti in variabili riservate. Mappatura a eVar, prop ed eventi non più necessari all&#39;interno del codice di implementazione. I clienti possono mappare i dati contestuali alle variabili utilizzando le regole di elaborazione. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | N/D | Non è più necessario in quanto la mappatura avviene tramite variabili riservate e regole di elaborazione. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | N/D | Non è più necessario in quanto la mappatura avviene tramite variabili riservate e regole di elaborazione. |

### Variabili facoltative

| Pietra miliare | Sintassi pietra miliare | Media Analytics | Sintassi di Media Analytics |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N/D | Non vengono più fornite mappature di lettore preconfigurate. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N/D | Non vengono più fornite mappature di lettore preconfigurate. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N/D | Content Complete (Completo contenuto) supporta solo un indicatore di avanzamento del 100%. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N/D | Content Complete (Completo contenuto) supporta solo un indicatore di avanzamento del 100%. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Chiave SDK: playerName;<br> Chiave API: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N/D | Media Analytics è impostato su 10 secondi per il contenuto e su 1 secondo per gli annunci. Non sono disponibili altre opzioni. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N/D | Media Analytics tiene sempre traccia dei marcatori di avanzamento a 10%, 25%, 50%, 75%, 95%. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Media Analytics tiene sempre traccia dei marcatori di avanzamento a 10%, 25%, 50%, 75%, 95%. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N/D | La traccia automatica non è più disponibile. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N/D | La traccia automatica non è più disponibile. |

### Variabili di tracciamento annunci

| Pietra miliare | Sintassi pietra miliare | Media Analytics | Sintassi di Media Analytics |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N/D | Media Analytics è impostato su 10 secondi per il contenuto e su 1 secondo per gli annunci. Non sono disponibili altre opzioni. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N/D | Gli indicatori di avanzamento non sono forniti per impostazione predefinita per gli annunci. Utilizza le metriche calcolate per creare indicatori di avanzamento e avanzamento. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Media Analytics è impostato su 1 secondo per gli annunci. Non sono disponibili altre opzioni. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N/D | La traccia automatica non è più disponibile. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N/D | La traccia automatica non è più disponibile. |

### Metodi del modulo multimediale

| Pietra miliare | Sintassi pietra miliare | Media Analytics | Sintassi di Media Analytics |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName | `mediaName`: (obbligatorio) Il nome del video come desiderate venga visualizzato nei rapporti video. | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength | `mediaLength`: (richiesto) Lunghezza del video in secondi. | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName | `mediaPlayerName`: (obbligatorio) Il nome del lettore multimediale utilizzato per visualizzare il video, così come si desidera venga visualizzato nei rapporti video. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name | `name`: (obbligatorio) Nome o ID dell’annuncio. | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length | `length`: (obbligatorio) Lunghezza dell’annuncio. | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName | `playerName`: (obbligatorio) Nome del lettore multimediale utilizzato per visualizzare l’annuncio. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName | `parentName`: Nome o ID del contenuto principale in cui l’annuncio è incorporato. | N/D | Ereditato automaticamente. |
| parentPod | `parentPod`: Posizione nel contenuto principale in cui è stato riprodotto l’annuncio. | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition | `parentPodPosition`: Posizione all’interno del contenitore in cui viene riprodotto l’annuncio. | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM | `CPM`: CPM o CPM crittografato (con il prefisso &quot;~&quot;) che si applica a questa riproduzione. | N/D | Non disponibile per impostazione predefinita in Media Analytics. |
| Media.click | `s.Media.click(name, offset)` | N/D | Utilizza una chiamata di analisi dei collegamenti personalizzata per tenere traccia dei clic. |
| Media.close | `s.Media.close(mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(name, offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(mediaName, mediaOffset)` | trackPause <br> o <br> trackEvent | `trackPause()` <br> o `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> o <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | Utilizzate metadati personalizzati o standard per impostare ulteriori variabili. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(mediaName)` | N/D | La frequenza delle chiamate di tracciamento viene impostata automaticamente. |

