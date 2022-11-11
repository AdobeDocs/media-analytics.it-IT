---
title: Scopri come migrare da Milestone a Media Analytics
description: Scopri come modificare le variabili Milestone in Metriche di Media Analytics e i metodi del modulo Milestone in sintassi Media Analytics.
uuid: fdc96146-af63-48ce-b938-c0ca70729277
exl-id: 655841ed-3a02-4e33-bbc9-46fb14302194
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 14%

---

# Migrazione da Milestone a Media Analytics {#migrating-from-milestone-to-media-analytics}

## Panoramica {#overview}

I concetti di base della misurazione video sono gli stessi per Milestone e Media Analytics, che sta prendendo gli eventi del lettore video e li mappando ai metodi di analisi, acquisendo anche i metadati e i valori del lettore e mappandoli alle variabili di analisi. La soluzione Media Analytics è nata da Milestone, quindi molti dei metodi e delle metriche sono gli stessi, tuttavia l&#39;approccio di configurazione e il codice sono cambiati in modo significativo. Dovrebbe essere possibile aggiornare il codice evento del lettore per puntare ai nuovi metodi di Media Analytics. Vedi [Panoramica SDK](/help/implementation/media-sdk/setup/setup-overview.md) e [Panoramica del tracciamento](/help/use-cases/track-av-playback/track-core-overview.md) per maggiori dettagli sull&#39;implementazione di Media Analytics.

Le tabelle seguenti forniscono traduzioni tra la soluzione Milestone e la soluzione Media Analytics.

## Guida alla migrazione {#migration-guide}

### Riferimento variabile

| Metrica Milestone | Tipo di variabile | Metrica di Media Analytics |
| --- | --- | --- |
| Contenuto | eVar <br> Scadenza predefinita: Visita | Contenuto |
| Tipo di contenuto | eVar <br> Scadenza predefinita: Vista a pagina | Tipo di contenuto |
| Tempo trascorso dei contenuti | Evento <br> Tipo: Contatore | Tempo trascorso dei contenuti |
| Avvio video | Evento <br> Tipo: Contatore | Avvio video |
| Completamento video | Evento <br> Tipo: Contatore | Completamento contenuto |


### Variabili del modulo multimediale

| Milestone | Sintassi Milestone | Media Analytics | Sintassi di Media Analytics |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | N/D | Tutti i dati di Media Analytics vengono inviati solo utilizzando i dati contestuali. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N/D | I dati contestuali di Media Analytics vengono compilati automaticamente in variabili riservate. Mappatura a eVar, prop ed eventi non più necessari all&#39;interno del codice di implementazione. I clienti possono mappare i dati contestuali alle variabili utilizzando le regole di elaborazione. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | N/D | Non più necessario in quanto la mappatura avviene tramite variabili riservate e regole di elaborazione. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | N/D | Non più necessario in quanto la mappatura avviene tramite variabili riservate e regole di elaborazione. |

### Variabili facoltative

| Milestone | Sintassi Milestone | Media Analytics | Sintassi di Media Analytics |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N/D | Non forniamo più mappature del lettore predefinite. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N/D | Non forniamo più mappature del lettore predefinite. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N/D | Il completamento del contenuto supporta solo un marcatore di avanzamento al 100%. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N/D | Il completamento del contenuto supporta solo un marcatore di avanzamento al 100%. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Chiave SDK: playerName;<br> Chiave API: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N/D | Media Analytics è impostato su 10 secondi per il contenuto e 1 secondo per gli annunci. Non sono disponibili altre opzioni. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N/D | Media Analytics tiene sempre traccia dei marcatori di avanzamento al 10%, 25%, 50%, 75%, 95%. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Media Analytics tiene sempre traccia dei marcatori di avanzamento al 10%, 25%, 50%, 75%, 95%. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N/D | La traccia automatica non è più disponibile. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N/D | La traccia automatica non è più disponibile. |

### Variabili di tracciamento degli annunci

| Milestone | Sintassi Milestone | Media Analytics | Sintassi di Media Analytics |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N/D | Media Analytics è impostato su 10 secondi per il contenuto e 1 secondo per gli annunci. Non sono disponibili altre opzioni. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N/D | Per impostazione predefinita, per gli annunci non sono disponibili marcatori di avanzamento. Utilizza le metriche calcolate per creare marcatori di avanzamento degli annunci. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Media Analytics è impostato a 1 secondo per gli annunci. Non sono disponibili altre opzioni. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N/D | La traccia automatica non è più disponibile. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N/D | La traccia automatica non è più disponibile. |

### Metodi del modulo multimediale

| Milestone | Sintassi Milestone | Media Analytics | Sintassi di Media Analytics |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName | `mediaName`: (obbligatorio) Il nome del video che desideri venga visualizzato nei rapporti video. | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength | `mediaLength`: (obbligatorio) La lunghezza del video in secondi. | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName | `mediaPlayerName`: (obbligatorio) Nome del lettore multimediale utilizzato per visualizzare il video, come desideri che appaia nei rapporti video. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name | `name`: (obbligatorio) Nome o ID dell’annuncio. | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length | `length`: (obbligatorio) La lunghezza dell’annuncio. | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName | `playerName`: (obbligatorio) Nome del lettore multimediale utilizzato per visualizzare l&#39;annuncio. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName | `parentName`: Nome o ID del contenuto principale in cui l’annuncio è incorporato. | N/D | Ereditato automaticamente. |
| parentPod | `parentPod`: Posizione nel contenuto principale dell’annuncio. | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition | `parentPodPosition`: Posizione all’interno del pod in cui viene riprodotto l’annuncio. | posizione | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM | `CPM`: CPM o CPM crittografato (con prefisso &quot;~&quot;) che si applica a questa riproduzione. | N/D | Non disponibile per impostazione predefinita in Media Analytics. |
| Media.click | `s.Media.click(name, offset)` | N/D | Utilizza una chiamata di analisi dei collegamenti personalizzata per tenere traccia dei clic. |
| Media.close | `s.Media.close(mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(name, offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(mediaName, mediaOffset)` | trackPause <br> o <br> trackEvent | `trackPause()` <br> o `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> o <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | Utilizza metadati personalizzati o standard per impostare variabili aggiuntive. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(mediaName)` | N/D | La frequenza di chiamata di tracciamento viene impostata automaticamente. |
