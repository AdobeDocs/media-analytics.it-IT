---
seo-title: Migrazione da Milestone ad Media Analytics
title: Migrazione da Milestone ad Media Analytics
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# Migrazione da Milestone ad Media Analytics {#migrating-from-milestone-to-media-analytics}

## Panoramica {#overview}

I concetti di base della misurazione video sono gli stessi per Milestone e Media Analytics, ovvero prendere gli eventi dei lettori video e mapparli ai metodi di analisi, acquisire anche i metadati e i valori dei lettori e mapparli alle variabili di analisi. La soluzione Media Analytics è nata da Milestone, quindi molti dei metodi e delle metriche sono gli stessi, ma l'approccio di configurazione e il codice sono cambiati in modo significativo. Dovrebbe essere possibile aggiornare il codice evento del lettore per puntare ai nuovi metodi di Media Analytics. Per ulteriori informazioni sull’implementazione di Media Analytics, consulta Panoramica [](/help/sdk-implement/setup/setup-overview.md) SDK e Panoramica sul [tracciamento](/help/sdk-implement/track-av-playback/track-core-overview.md) .

Le tabelle seguenti contengono le traduzioni tra la soluzione Milestone e la soluzione Media Analytics.

## Migration guide {#migration-guide}

### Riferimento variabile

| Metrica cardine | Tipo di variabile | Metrica di Media Analytics |
| --- | --- | --- |
| Contenuto | Scadenza<br/><br/>eVarDefault: Visita | Contenuto |
| Tipo di contenuto | eVar<br/><br/> Default expiration: Page view | Tipo di contenuto |
| Tempo contenuto trascorso | Tipo evento<br/><br/> : Contatore | Tempo contenuto trascorso |
| Avvio video | Tipo evento<br/><br/> : Contatore | Avvio video |
| Completamento video | Tipo evento<br/><br/> : Contatore | Content Complete |

### Variabili del modulo multimediale

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintassi pietra miliare
</th>
<th>Media Analytics
</th>
<th>Sintassi di Media Analytics
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.trackUsingContextData
</td>
<td>
<pre>
s.Media.trackUsingContextData = true;
</pre>
</td>
<td>N/D
</td>
<td>Tutti i dati di Media Analytics vengono inviati solo utilizzando i dati contestuali.
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = { "a.media.name":"eVar2,prop2", "a.media.segment":"eVar3", "a.contentType":"eVar1", "a.media.timePlayed":"event3", "a.media.view":"event1", "a.media.segmentView":"event2", "a.media.complete":"event7", "a.media.milestones": { 25:"event4", 50:"event5", 75:"event6" }};
</pre>
</td>
<td>N/D
</td>
<td>I dati contestuali di Media Analytics vengono inseriti automaticamente nelle variabili memorizzate. Mappatura a eVar, prop ed eventi non più necessari all'interno del codice di implementazione. I clienti possono mappare i dati di contesto alle variabili utilizzando le regole di elaborazione.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars = "events, prop2, eVar1, eVar2, eVar3";
</pre>
</td>
<td>N/D
</td>
<td>Non è più necessario in quanto la mappatura avviene tramite variabili riservate e regole di elaborazione.
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents = "event1, event2, event3, event4, event5, event6, event7"
</pre>
</td>
<td>N/D
</td>
<td>Non è più necessario in quanto la mappatura avviene tramite variabili riservate e regole di elaborazione.
</td>
</tr>
</tbody>
</table>

### Variabili facoltative

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintassi pietra miliare
</th>
<th>Media Analytics
</th>
<th>Sintassi di Media Analytics
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.autoTrack
</td>
<td>
<pre>
s.Media.autoTrack = true;
</pre>
</td>
<td>N/D
</td>
<td>Non vengono più fornite mappature di lettore preconfigurate.
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.
  autoTrackNetStreams = true
</pre>
</td>
<td>N/D
</td>
<td>Non vengono più fornite mappature di lettore preconfigurate.
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.
  completeByCloseOffset = true
</pre>
</td>
<td>N/D
</td>
<td>Content Complete (Completo contenuto) supporta solo un indicatore di avanzamento del 100%.
</td>
</tr>
<tr>
<td>
Media.completeCloseOffsetThreshold
</td>
<td>
<pre>
s.Media.
  completeCloseOffsetThreshold = 1
</pre>
</td>
<td>N/D
</td>
<td>Content Complete (Completo contenuto) supporta solo un indicatore di avanzamento del 100%.
</td>
</tr>
<tr>
<td>
Media.playerName
</td>
<td>
<pre>
s.Media.playerName = "Nome lettore personalizzato"
</pre>
</td>
<td>
Chiave SDK: playerName; 
Chiave API: media.playerName
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</p>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.
  trackSeconds = 15
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics è impostato su 10 secondi per il contenuto e su 1 secondo per il contenuto. Non sono disponibili altre opzioni.
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.
  trackMilestones = "25,50,75";
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics tiene sempre traccia dei marcatori di avanzamento a 10%, 25%, 50%, 75%, 95%
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  trackOffsetMilestones = "20,40,60";
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics tiene sempre traccia dei marcatori di avanzamento a 10%, 25%, 50%, 75%, 95%
</td>
</tr>
<tr>
<td>
Media.segmentByMilestones
</td>
<td>
<pre>
s.Media.segmentByMilestones = true;
</pre>
</td>
<td>N/D
</td>
<td>La traccia automatica non è più disponibile
</td>
</tr>
<tr>
<td>
Media.segmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  segmentByOffsetMilestones = true;
</pre>
</td>
<td>N/D
</td>
<td>La traccia automatica non è più disponibile
</td>
</tr>
</tbody>
</table>

### Variabili di tracciamento annunci

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintassi pietra miliare
</th>
<th>Media Analytics
</th>
<th>Sintassi di Media Analytics
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.adTrackSeconds
</td>
<td>
<pre>
s.Media.
  adTrackSeconds = 15
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics è impostato su 10 secondi per il contenuto e su 1 secondo per il contenuto. Non sono disponibili altre opzioni.
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.
  adTrackMilestones = "25,50,75";
</pre>
</td>
<td>N/D
</td>
<td>Gli indicatori di avanzamento non sono forniti per impostazione predefinita per gli annunci. Metriche calcolate per creare marcatori di avanzamento annunci.
</td>
</tr>
<tr>
<td>
Media.adTrackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adTrackOffsetMilestones = "20,40,60";
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics è impostato su 1 secondo per gli annunci. Non sono disponibili altre opzioni.
</td>
</tr>
<tr>
<td>
Media.adSegmentByMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByMilestones = true;
</pre>
</td>
<td>N/D
</td>
<td>La traccia automatica non è più disponibile
</td>
</tr>
<tr>
<td>
Media.adSegmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByOffsetMilestones = true;
</pre>
</td>
<td>N/D
</td>
<td>La traccia automatica non è più disponibile
</td>
</tr>
</tbody>
</table>

### Metodi del modulo multimediale

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintassi pietra miliare
</th>
<th>Media Analytics
</th>
<th>Sintassi di Media Analytics
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.open
</td>
<td>
<pre>
s.Media.open( mediaName, mediaLength, mediaPlayerName)
</pre>
</td>
<td>
<pre>
trackSessionStart
</pre>
</td>
<td>
<pre>
trackSessionStart( mediaObject, contextData)
</pre>
</td>
</tr>
<tr>
<td>
mediaName - (Obbligatorio) Il nome del video come desiderate venga visualizzato nei rapporti video.
</td>
<td>
<pre>
mediaName
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createMediaObject( nome, mediaId, lunghezza, streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaLength - (Obbligatorio) La lunghezza del video in secondi.
</td>
<td>
<pre>
mediaLength
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createMediaObject( nome, mediaId, lunghezza, streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName - (Obbligatorio) Il nome del lettore multimediale utilizzato per visualizzare il video, così come si desidera venga visualizzato nei rapporti video.
</td>
<td>
<pre>
mediaPlayerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
Media.openAd
</td>
<td>
<pre>
s.Media.openAd( nome, lunghezza, nomeLettore, nomePadre, contenitorePadre, posizionePodPadre, CPM)
</pre>
</td>
<td>
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
mediaHeartbeat.trackEvent( MediaHeartbeat.
    Evento.
    AdBreakStart, adBreakObject);...
trackEvent( MediaHeartbeat.
    Evento.
    AdStart, adObject, adCustomMetadata);
</pre>
</td>
</tr>
<tr>
<td>
name - (Obbligatorio) Il nome o l'ID dell'annuncio.
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createAdObject( nome, adId, posizione, lunghezza)
</pre>
</td>
</tr>
<tr>
<td>
length(Obbligatorio) La lunghezza dell'annuncio.
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createAdObject( nome, adId, posizione, lunghezza)
</pre>
</td>
</tr>
<tr>
<td>
playerName - (Obbligatorio) Il nome del mediaplayer utilizzato per visualizzare l'annuncio.
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
parentName - Il nome o l'ID del contenuto principale in cui l'annuncio è incorporato.
</td>
<td>
<pre>
parentName
</pre>
</td>
<td>N/D
</td>
<td>ereditato automaticamente
</td>
</tr>
<tr>
<td>
parentPod - La posizione nel contenuto principale in cui è stato riprodotto l'annuncio.
</td>
<td>
<pre>
parentPod
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
createAdBreakObject( nome, posizione, oraInizio)
</pre>
</td>
</tr>
<tr>
<td>
parentPodPosition - La posizione all'interno del contenitore in cui viene riprodotto l'annuncio.
</td>
<td>
<pre>
parentPodPosition
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
createAdObject( nome, adId, posizione, lunghezza)
</pre>
</td>
</tr>
<tr>
<td>
CPMTil CPM o CPM crittografato (con il prefisso "~") che si applica a questa riproduzione.
</td>
<td>
<pre>
CPM
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile per impostazione predefinita in Media Analytics
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click( nome, offset)
</pre>
</td>
<td>N/D
</td>
<td>Utilizza una chiamata di analisi dei collegamenti personalizzata per tenere traccia dei clic
</td>
</tr>
<tr>
<td>
Media.close
</td>
<td>
<pre>
s.Media.close( mediaName)
</pre>
</td>
<td>
<pre>
trackSessionEnd
</pre>
</td>
<td>
<pre>
trackSessionEnd()
</pre>
</td>
</tr>
<tr>
<td>
Media.complete
</td>
<td>
<pre>
s.Media.complete( nome, offset)
</pre>
</td>
<td>
<pre>
trackComplete
</pre>
</td>
<td>
<pre>
trackComplete()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.play
</pre>
</td>
<td>
<pre>
s.Media.play( nome, offset, segmentoNum, segmento, segmentoLunghezza)
</pre>
</td>
<td>
<pre>
trackPlay
</pre>
</td>
<td>
<pre>
trackPlay()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.stop
</pre>
</td>
<td>
<pre>
s.Media.stop( mediaName, mediaOffset)
</pre>
</td>
<td>
<pre>
trackPause
</pre>  oppure  
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
trackPause()
</pre> 
 oppure 
<pre>

trackEvent( MediaHeartbeat.
  Evento.
  SeekStart)
</pre>  oppure 
<pre>

trackEvent( MediaHeartbeat.
  Evento.
  BufferStart);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.monitor
</pre>
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>Utilizzare metadati personalizzati o standard per impostare ulteriori variabili
</td>
<td>
<pre>
var customVideoMetadata = { isUserLoggedIn: 
    "false", tvStation: 
    "Stazione TV di esempio", programmatore: 
    "Sample programer"};...
var standardVideoMetadata = {};
standardVideoMetadata [MediaHeartbeat.
   VideoMetadataKeys.
   EPISODE] = "Esempio di episodio";
standardVideoMetadata [MediaHeartbeat.
   VideoMetadataKeys.
   SHOW] = "Sample Show";...
mediaObject.setValue( MediaHeartbeat.
  MediaObjectKey.
  StandardVideoMetadata, standardVideoMetadata);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.track
</pre>
</td>
<td>
<pre>
s.Media.track( mediaName)
</pre>
</td>
<td>N/D
</td>
<td>La frequenza delle chiamate di tracciamento viene impostata automaticamente.
</td>
</tr>
</tbody>
</table>

