---
title: Informazioni sulla migrazione da Milestone al collegamento personalizzato
description: Scopri come modificare le variabili Milestone nei metodi del modulo del collegamento personalizzato e Milestone nella sintassi del collegamento personalizzato.
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
exl-id: 732079f4-3eb8-4b9a-892b-25a1c9332be4
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 100%

---

# Migrazione da Milestone al collegamento personalizzato{#migrating-from-milestone-to-custom-link}

## Panoramica {#overview}

I concetti di base della misurazione video sono gli stessi per il tracciamento Milestone e del collegamento personalizzato, ovvero l’acquisizione degli eventi del lettore video e la relativa mappatura sui metodi Analytics, nonché l’acquisizione dei metadati e dei valori del lettore e la relativa mappatura sulle variabili Analytics. L’approccio al collegamento personalizzato deve essere considerato come una velocizzazione e una semplificazione sia dell’implementazione che dei dati raccolti. Con il collegamento personalizzato non è possibile predefinire variabili o metodi per la misurazione video, ma è necessaria una configurazione completamente personalizzata. Dovrebbe essere possibile aggiornare il codice evento del lettore per indicare le chiamate di tracciamento dei collegamenti personalizzati per gli eventi di base del lettore, come Avvia e Completa. Per ulteriori dettagli, consulta la [Guida all’implementazione del collegamento personalizzato](/help/legacy/measurement-options/cl-in-aa/cl-impl-guide.md).

Le tabelle seguenti forniscono traduzioni tra la soluzione Milestone e la soluzione collegamento personalizzato.

## Guida alla migrazione {#migration-guide}

### Riferimento a una variabile video

| Metrica Milestone | Tipo di variabile | Collegamento personalizzato |
| --- | --- | --- |
| Contenuto |  Scadenza predefinita eVar<br>: visita | Definisci la tua eVar. |
| Tipo di contenuto | Scadenza predefinita eVar <br>: visualizzazione pagina | Definisci la tua eVar. |
| Tempo trascorso dei contenuti | Tipo di <br>evento: contatore | Definisci il tuo evento. |
| Inizia video | Tipo di <br>evento: contatore | Definisci il tuo evento. |
| Completamento video | Tipo di <br>evento: contatore | Definisci il tuo evento. |

### Variabili del modulo multimediale

| Milestone | Sintassi di Milestone | Collegamento personalizzato | Sintassi del collegamento personalizzato |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `  contextData.video.name’;` <br> `  s.contextData["video.name"]` <br> `  = mediaName;` |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N/D | La mappatura dei dati contestuali a eVar, prop ed eventi ora viene completata tramite regole di elaborazione. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `    prop10,` <br> `    eVar10,` <br> `    eVar12,` <br> `    eVar13,` <br> `    eVar15,` <br> `    contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> |
| media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | linkTrackEvents | `s.linkTrackEvents` <br> `  = 'event2';` |

### Variabili facoltative

| Milestone | Sintassi di Milestone | Collegamento personalizzato | Sintassi del collegamento personalizzato |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N/D | Non disponibile. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N/D | Non disponibile. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N/D | Non disponibile. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N/D | Non disponibile. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Imposta l’eVar o la variabile dei dati di contesto nella chiamata del collegamento. | `s.contextData['video.player']` <br> `  = "CustomPlayer Name";` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N/D | Non disponibile. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N/D | Non disponibile. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Non disponibile. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N/D | Non disponibile. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N/D | Non disponibile. |

### Variabili di tracciamento degli annunci

| Milestone | Sintassi di Milestone | Collegamento personalizzato | Sintassi del collegamento personalizzato |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N/D | Non disponibile. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N/D | Non disponibile. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Non disponibile. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N/D | Non disponibile. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N/D | Non disponibile. |

### Metodi del modulo multimediale

| Milestone | Sintassi di Milestone | Collegamento personalizzato | Sintassi del collegamento personalizzato |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.view';` <br> `s.linkTrackEvents ` <br> `  = 'event2';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event2';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.view']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Start');` |
| mediaName | `mediaName`: (obbligatorio) il nome del video come desideri che venga visualizzato nei rapporti video. | Imposta l’eVar o la variabile dei dati di contesto nella chiamata del collegamento. | `s.prop10 = mediaName;` <br> `s.eVar10 = mediaName;` <br> `s.contextData['video.name']` <br> `  = mediaName;` |
| mediaLength | `mediaLength`: (obbligatorio) la durata del video in secondi. | Imposta l’eVar o la variabile dei dati di contesto nella chiamata del collegamento. | `s.contextData['video.length']` <br> `  = "90";` |
| mediaPlayerName | `mediaPlayerName`: (obbligatorio) il nome del lettore multimediale utilizzato per visualizzare il video, come desideri che venga visualizzato nei rapporti video. | Imposta l’eVar o la variabile dei dati di contesto nella chiamata del collegamento. | `s.contextData['video.player']` <br> `  = "CustomPlayer Name";` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | N/D | Non disponibile. |
| name | `name`: (obbligatorio) il nome o l’ID dell’annuncio. | N/D | Non disponibile. |
| length | `length`: (obbligatorio) la durata dell’annuncio. | N/D | Non disponibile. |
| playerName | `playerName`: (obbligatorio) il nome del lettore multimediale utilizzato per visualizzare l’annuncio. | N/D | Non disponibile. |
| parentName | `parentName`: il nome o l’ID del contenuto principale in cui l’annuncio è incorporato. | N/D | Non disponibile. |
| parentPod | `parentPod`: la posizione nel contenuto principale in cui è stato riprodotto l’annuncio. | N/D | Non disponibile. |
| parentPodPosition | `parentPodPosition`: la posizione all’interno del pod in cui viene riprodotto l’annuncio. | N/D | Non disponibile. |
| CPM | `CPM`: il CPM o il CPM crittografato (con prefisso “~”) che si applica a questa riproduzione. | N/D | Non disponibile. |
| Media.click | `s.Media.click(name, offset)` | `s.tl()` | Utilizza una chiamata Analytics del collegamento personalizzato per tenere traccia dei clic. |
| Media.close | `s.Media.close(mediaName)` | N/D | Non disponibile. |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.complete';` <br> `s.linkTrackEvents ` <br> `  = 'event3';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event3';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.complete']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Complete');` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | N/D | Non disponibile. |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | N/D | Non disponibile. |
| Media.monitor | `s.Media.monitor(s, media)` | Imposta l’eVar o la variabile dei dati di contesto nella chiamata del collegamento. | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> `s.linkTrackEvents = 'event2';` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | N/D | Non disponibile. |
