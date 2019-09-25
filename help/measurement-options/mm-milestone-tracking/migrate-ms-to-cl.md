---
seo-title: Migrazione da attività cardine a collegamento personalizzato
title: Migrazione da attività cardine a collegamento personalizzato
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Migrazione da attività cardine a collegamento personalizzato{#migrating-from-milestone-to-custom-link}

## Panoramica {#section_xlc_fc2_dfb}

I concetti di base della misurazione video sono gli stessi per il tracciamento Milestone e Custom Link, che consiste nell’eseguire gli eventi dei lettori video e nel mapparli ai metodi di analisi, nonché acquisire i metadati e i valori dei lettori e mapparli alle variabili di analisi. L'approccio "Custom Link" dovrebbe essere considerato un modo per ridurre e semplificare sia l'attuazione che i dati raccolti. Con la soluzione Custom Link, per la misurazione video non sono predefiniti variabili o metodi, ma è necessaria una configurazione completa e personalizzata. Dovrebbe essere possibile aggiornare il codice evento del lettore in modo che punti alle chiamate di tracciamento dei collegamenti personalizzate per gli eventi del lettore di base, come start e complete. Per ulteriori informazioni, consulta la guida [all’implementazione dei collegamenti](/help/measurement-options/cl-in-aa/cl-impl-guide.md) personalizzati e il tracciamento [manuale dei collegamenti tramite codice](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html) di collegamento personalizzato.

Le tabelle seguenti contengono le traduzioni tra la soluzione Milestone e la soluzione Custom Link.

## Migration guide {#section_btt_fc2_dfb}

### Riferimento per la variabile video

<table>
<thead>
<tr>
<th><strong>Metrica cardine</strong></th>
<th><strong>Tipo di variabile</strong></th>
<th><strong>Collegamento personalizzato</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>Contenuto</td>
<td>
<p>eVar</p>
<p>Scadenza predefinita: visita</p>
</td>
<td>Definisci la tua eVar</td>
</tr>
<tr>
<td>Tipo di contenuto</td>
<td>
<p>eVar</p>
<p>Scadenza predefinita: visualizzazioni pagina</p>
</td>
<td>Definisci la tua eVar</td>
</tr>
<tr>
<td>Tempo contenuto trascorso</td>
<td>
<p>Evento</p>
<p>Tipo: contatore</p>
</td>
<td>Definire un proprio evento</td>
</tr>
<tr>
<td>Avvio video</td>
<td>
<p>Evento</p>
<p>Tipo: contatore</p>
</td>
<td>Definire un proprio evento</td>
</tr>
<tr>
<td>Completamento video</td>
<td>
<p>Evento</p>
<p>Tipo: contatore</p>
</td>
<td>Definire un proprio evento</td>
</tr>
</tbody>
</table>

### Variabili del modulo multimediale

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintassi pietra miliare
</th>
<th>Collegamento personalizzato
</th>
<th>Sintassi collegamento personalizzata
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
s.Media.
  trackUsingContextData = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, contextData.video.name'; 
s.contextData[‘video.name’] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.
  contextDataMapping = { "a.media.name":
    "eVar2,prop2", "a.media.segment":
    "eVar3", "a.contentType":
    "eVar1", "a.media.timePlayed":
    "event3", "a.media.view":
    "event1", "a.media.segmentView":
    "event2", "a.media.complete":
    "event7", "a.media.milestones":{ 25:"event4", 50:"event5", 75:"event6" }};
</pre>
</td>
<td>N/D
</td>
<td>La mappatura dei dati contestuali su eVar, prop ed eventi ora viene completata attraverso le regole di elaborazione.
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
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15, contextData.
       video.name, contextData.
       video.view';
</pre>
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
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintassi pietra miliare
</th>
<th>Collegamento personalizzato
</th>
<th>Sintassi collegamento personalizzata
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
s.Media.
  trackUsingContextData = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, contextData.video.name'; 
s.contextData[‘video.name’] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = { "a.media.name":"eVar2,prop2", "a.media.segment":"eVar3", "a.contentType":"eVar1", "a.media.timePlayed":"event3", "a.media.view":"event1", "a.media.segmentView":"event2", "a.media.complete":"event7", "a.media.milestones":{ 25:"event4", 50:"event5", 75:"event6" }};
</pre>
</td>
<td>N/D
</td>
<td>La mappatura dei dati contestuali su eVar, prop ed eventi ora viene completata attraverso le regole di elaborazione.
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
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15, contextData.
       video.name, contextData.
       video.view';
</pre>
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
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents = 'event2';
</pre>
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
<th>Collegamento personalizzato
</th>
<th>Sintassi collegamento personalizzata
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
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.autoTrackNetStreams = true
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.completeByCloseOffset = true
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
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
<td>Non disponibile
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
Imposta eVar o variabile di dati di contesto nella chiamata di collegamento
</td>
<td>
<pre>
s.contextData['video.player'] ="CustomPlayer Name";
</pre>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.trackSeconds = 15
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.trackMilestones = "25,50,75";
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.trackOffsetMilestones = "20,40,60";
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
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
<td>Non disponibile
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
<td>Non disponibile
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
<th>Collegamento personalizzato
</th>
<th>Sintassi collegamento personalizzata
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
s.Media.adTrackSeconds = 15 
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.adTrackMilestones = "25,50,75";
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
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
<td>Non disponibile
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
<td>Non disponibile
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
<td>Non disponibile
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
<th>Collegamento personalizzato
</th>
<th>Sintassi collegamento personalizzata
</th>
</tr>
</thead>
<tbody>
<tr>
<td>Media.open</td>
<td>
<pre>
s.Media.open( mediaName, mediaLength, mediaPlayerName)
</pre>
</td>
<td>s.tl()</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData.video.name, contextData.video.view';
s.linkTrackEvents = 'event2';
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.eVar12 = "video";
s.eVar15 = mediaPlayerName;
s.events = 'event2';
s.contextData['video.name'] = mediaName;
s.contextData['video.view'] = 'true';
s.tl(this,'o','Video Start');
</pre>
</td>
</tr>
<tr>
<td>mediaName</td>
<td><b></b> mediaName: (obbligatorio) Il nome del video come desiderate venga visualizzato nei rapporti video.</td>
<td>Imposta eVar o variabile di dati di contesto nella chiamata di collegamento</td>
<td>
<pre>
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.contextData['video.name'] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
mediaLength
</td>
<td>
<b></b> mediaLength: (richiesto) Lunghezza del video in secondi.
</td>
<td>
Imposta eVar o variabile di dati di contesto nella chiamata di collegamento
</td>
<td>
<pre>
s.contextData['video.length'] ="90";
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName
</td>
<td>
<b></b> mediaPlayerName: (obbligatorio) Il nome del lettore multimediale utilizzato per visualizzare il video, così come lo si desidera, nei rapporti video.
</td>
<td>
Imposta eVar o variabile di dati di contesto nella chiamata di collegamento
</td>
<td>
<pre>
s.contextData['video.player'] ="CustomPlayer Name";
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
<td>N/D
</td>
<td>Non disponibile</td>
</tr>
<tr>
<td>name</td>
<td><b></b> name: (obbligatorio) Nome o ID dell’annuncio.</td>
<td>N/D</td>
<td>Non disponibile</td>
</tr>
<tr>
<td>
length
</td>
<td>
<b></b> lunghezza: (obbligatorio) Lunghezza dell’annuncio.
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
playerName
</td>
<td>
<b></b> playerName: (obbligatorio) Nome del lettore multimediale utilizzato per visualizzare l’annuncio.
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
parentName
</td>
<td>
<b></b> parentName: Nome o ID del contenuto principale in cui l’annuncio è incorporato.
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
parentPod
</td>
<td>
<b></b> parentPod: La posizione nel contenuto principale in cui è stata riprodotta l’annuncio.
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
parentPodPosition
</td>
<td>
<b></b> parentPodPosition: Posizione all’interno del contenitore in cui viene riprodotto il tead.
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
CPM
</td>
<td>
<b></b> CPM: CPM o CPM crittografato (con il prefisso "~") che si applica a questa riproduzione.
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click(nome, offset)
</pre>
</td>
<td>
<pre>
s.tl()
</pre>
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
s.Media.close(mediaName)
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
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
s.tl()
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData.
       video.name, contextData.
       video.complete";
s.linkTrackEvents = 'event3';
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.eVar12 = "video";
s.eVar15 = mediaPlayerName;
s.events = 'event3';
s.contextData['video.name'] = mediaName;
s.contextData['video.complete'] = 'true';
s.tl(this,'o','Video Complete');
</pre>
</td>
</tr>
<tr>
<td>
Media.play
</td>
<td>
<pre>
s.Media.play( nome, offset, segmentoNum, segmento, segmentoLunghezza)
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media.stop
</td>
<td>
<pre>
s.Media.stop( mediaName, mediaOffset)
</pre>
</td>
<td>N/D 
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media.monitor
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>
Imposta eVar o variabile di dati di contesto nella chiamata di collegamento
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData.
       video.name, contextData.
       video.view';
s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
<tr>
<td>
Media.track
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
</tbody>
</table>

