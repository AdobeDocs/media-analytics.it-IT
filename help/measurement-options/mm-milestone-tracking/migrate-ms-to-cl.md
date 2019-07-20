---
seo-title: Migrazione da milestone a Custom Link (Migrazione da pietra miliare a collegamento personalizzato)
title: Migrazione da milestone a Custom Link (Migrazione da pietra miliare a collegamento personalizzato)
uuid: 1 c 8 edde 5-0 ef 1-4 bc 0-a 62 d -1747 f 4907 f 09
translation-type: tm+mt
source-git-commit: 530973abc12fcb2567a3742c202d992944048b8b

---


# Migrating from Milestone to Custom Link{#migrating-from-milestone-to-custom-link}

## Panoramica {#section_xlc_fc2_dfb}

I concetti principali della misurazione video sono identici per i tracciamenti milestone (Pietra miliare) e Custom Links (Tracciamento collegamenti personalizzati), che occupano eventi del lettore video e li mappano sui metodi di analisi, e li mappano anche sui metadati e i valori del lettore, e mappandoli alle variabili di analisi. L'approccio Collegamento personalizzato deve essere considerato come sliminare e semplificare sia l'implementazione che i dati raccolti. Con la soluzione Custom Link (Collegamento personalizzato), nessuna variabile o metodo è predefinito per la misurazione video, richiede una configurazione personalizzata completa. Dovrebbe essere possibile aggiornare il codice dell'evento del lettore in modo che punti alle chiamate di tracciamento dei collegamenti personalizzate per eventi di base quali avvio e completamento. See [Custom Link implementation guide](../../measurement-options/cl-in-aa/cl-impl-guide.md) and [Manual Link Tracking Using Custom Link Code](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html) for more details.

Le tabelle seguenti forniscono traduzioni tra la soluzione Milestone (Pietra miliare) e la soluzione Custom Link (Collegamento personalizzato).

## Migration guide {#section_btt_fc2_dfb}

### Riferimento variabile video

<table>
<thead>
<tr>
<th><strong>Milestone Metric (Metrica milestone Metrica)</strong></th>
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
<td>Definire la tua evar</td>
</tr>
<tr>
<td>Tipo di contenuto</td>
<td>
<p>eVar</p>
<p>Scadenza predefinita: visualizzazioni pagina</p>
</td>
<td>Definire la tua evar</td>
</tr>
<tr>
<td>Tempo contenuto trascorso</td>
<td>
<p>Evento</p>
<p>Tipo: contatore</p>
</td>
<td>Definire un evento personale</td>
</tr>
<tr>
<td>Video avviato</td>
<td>
<p>Evento</p>
<p>Tipo: contatore</p>
</td>
<td>Definire un evento personale</td>
</tr>
<tr>
<td>Completamenti video</td>
<td>
<p>Evento</p>
<p>Tipo: contatore</p>
</td>
<td>Definire un evento personale</td>
</tr>
</tbody>
</table>

### Variabili modulo Media

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintassi milestone (Pietra miliare)
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
Media. trackusingcontextdata
</td>
<td>
<pre>
s. Media.
 Trackusingcontextdata 
 = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 ='events, 
contextdata. video. namè; 
s. contextdata ['video. namè]
 = medianame;
</pre>
</td>
</tr>
<tr>
<td>
Media. contextdatamapping
</td>
<td>
<pre>
s. Media.
 Contextdatamapping = {"a. media. name":
 " Evar 2, prop 2 ","
 a. media. segment ":
 " Evar 3 ","
 a. contenttype ":
 " Evar 1 ","
 a. media. timeplayed ":
 " event 3 ","
 a. media. view ":
 " event 1 ","
 a. media. segmentview ":
 " event 2 ","
 a. media. complete ":
 " event 7 ","
 a. media. milestones ": {25: " event 4 ",
 50: " event 5 ",
 75: " event 6 "}};
</pre>
</td>
<td>N/D
</td>
<td>La mappatura dei dati contestuali a evar, prop ed eventi ora viene completata
tramite le regole di elaborazione.
</td>
</tr>
<tr>
<td>
Media. trackvars
</td>
<td>
<pre>
s. Media. trackvars
 = "events,
 prop 2,
 evar 1,
 evar 2,
 evar 3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 ='events,
 prop 10,
 evar 10,
 evar 12,
 evar 13,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. view ';
</pre>
</td>
</tr>
<tr>
<td>
Media. trackevents
</td>
<td>
<pre>
s. Media. trackevents
 = "event 1,
 event 2,
 event 3,
 event 4,
 event 5,
 event 6,
 event 7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s. linktrackevents
 ='event 2 ';
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
<th>Sintassi milestone (Pietra miliare)
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
Media. trackusingcontextdata
</td>
<td>
<pre>
s. Media.
 Trackusingcontextdata 
 = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 ='events, 
contextdata. video. namè; 
s. contextdata ['video. namè]
 = medianame;
</pre>
</td>
</tr>
<tr>
<td>
Media. contextdatamapping
</td>
<td>
<pre>
s. Media. contextdatamapping = {"a. media. name": " Evar 2, prop 2 ","
 a. media. segment ": " Evar 3 ","
 a. contenttype ": " Evar 1 ","
 a. media. timeplayed ": " event 3 ","
 a. media. view ": " event 1 ","
 a. media. segmentview ": " event 2 ","
 a. media. complete ": " event 7 ","
 a. media. milestones ": {25: " event 4 ",
 50: " event 5 ",
 75: " event 6 "}};
</pre>
</td>
<td>N/D
</td>
<td>La mappatura dei dati contestuali a evar, prop ed eventi ora viene completata
tramite le regole di elaborazione.
</td>
</tr>
<tr>
<td>
Media. trackvars
</td>
<td>
<pre>
s. Media. trackvars
 = "events,
 prop 2,
 evar 1,
 evar 2,
 evar 3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 ='events,
 prop 10,
 evar 10,
 evar 12,
 evar 13,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. view ';
</pre>
</td>
</tr>
<tr>
<td>
Media. trackevents
</td>
<td>
<pre>
s. Media. trackevents
 = "event 1,
 event 2,
 event 3,
 event 4,
 event 5,
 event 6,
 event 7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s. linktrackevents
 ='event 2 ';
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
<th>Sintassi milestone (Pietra miliare)
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
Media. autotrack
</td>
<td>
<pre>
s. Media. autotrack
 = true;
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media. autotracknetstreams
</td>
<td>
<pre>
s. Media. autotracknetstreams
 = true
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media. completebycloseoffset
</td>
<td>
<pre>
s. Media. completebycloseoffset
 = true
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media. completecloseoffsetthreshold
</td>
<td>
<pre>
s. Media.
 Completecloseoffsetthreshold
 = 1
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media. playername
</td>
<td>
<pre>
s. Media. playername 
 = "Nome lettore personalizzato"
</pre>
</td>
<td>
Imposta variabile di dati evar o di contesto nella chiamata di collegamento
</td>
<td>
<pre>
s. contextdata ['video. player ']
 =» customplayer Name»;
</pre>
</td>
</tr>
<tr>
<td>
Media. trackseconds
</td>
<td>
<pre>
s. Media. trackseconds = 15
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media. trackmilestones
</td>
<td>
<pre>
s. Media. trackmilestones 
 = "25,50,75";
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media. trackoffsetmilestones
</td>
<td>
<pre>
s. Media. trackoffsetmilestones 
 = "20,40,60";
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media. segmentbymilestones
</td>
<td>
<pre>
s. Media. segmentbymilestones
 = true;
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media. segmentbyoffsetmilestones
</td>
<td>
<pre>
s. Media.
 Segmentbyoffsetmilestones
 = true;
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
<th>Sintassi milestone (Pietra miliare)
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
Media. adtrackseconds
</td>
<td>
<pre>
s. Media. adtrackseconds 
 = 15 
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media. adtrackmilestones
</td>
<td>
<pre>
s. Media. adtrackmilestones 
 = "25,50,75";
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media. adtrackoffsetmilestones
</td>
<td>
<pre>
s. Media.
 Adtrackoffsetmilestones 
 = "20,40,60";
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media. adsegmentbymilestones
</td>
<td>
<pre>
s. Media.
 Adsegmentbymilestones
 = true;
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media. adsegmentbyoffsetmilestones
</td>
<td>
<pre>
s. Media.
 Adsegmentbyoffsetmilestones
 = true;
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
</tbody>
</table>

### Metodi modulo Media

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintassi milestone (Pietra miliare)
</th>
<th>Collegamento personalizzato
</th>
<th>Sintassi collegamento personalizzata
</th>
</tr>
</thead>
<tbody>
<tr>
<td>File multimediali. open</td>
<td>
<pre>
s. Media. open (medianame,
 medialength,
 mediaplayername)
</pre>
</td>
<td>s. tl ()</td>
<td>
<pre>
s. linktrackvars
 ='events,
 prop 10,
 evar 10,
 evar 12,
 evar 15,
 contextdata. video. name,
 contextdata. video. view ';
s. linktrackevents 
 ='event 2 ';
s. prop 10 
 = Medianame;
s. evar 10 
 = Medianame;
s. evar 12 
 = "video";
s. evar 15 
 = Mediaplayername;
s. events 
 ='event 2 ';
s. contextdata ['video. namè] 
 = Medianame;
s. contextdata ['video. view '] 
 ='truè;
s. tl (this,'o ','Video Start ');
</pre>
</td>
</tr>
<tr>
<td>Medianame</td>
<td><b>Medianame:</b> (obbligatorio) Il nome del video che viene visualizzato nei rapporti video.</td>
<td>Imposta variabile di dati evar o di contesto nella chiamata di collegamento</td>
<td>
<pre>
s. prop 10 = medianame;
s. evar 10 = medianame;
s. contextdata ['video. namè]
 = medianame;
</pre>
</td>
</tr>
<tr>
<td>
Medialength
</td>
<td>
<b>Medialength:</b> (obbligatorio) La lunghezza del video in secondi.
</td>
<td>
Imposta variabile di dati evar o di contesto nella chiamata di collegamento
</td>
<td>
<pre>
s. contextdata ['video. length ']
 =» 90»;
</pre>
</td>
</tr>
<tr>
<td>
Mediaplayername
</td>
<td>
<b>Mediaplayername:</b> (obbligatorio) Il nome del lettore
multimediale utilizzato per visualizzare il video, in modo che venga visualizzato nei rapporti video.
</td>
<td>
Imposta variabile di dati evar o di contesto nella chiamata di collegamento
</td>
<td>
<pre>
s. contextdata ['video. player ']
 =» customplayer Name»;
</pre>
</td>
</tr>
<tr>
<td>
Media. openad
</td>
<td>
<pre>
s. Media. openad (nome,
 lunghezza,
 playername,
 parentname,
 parentpod,
 parentpodposition,
 CPM)
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile</td>
</tr>
<tr>
<td>name</td>
<td><b>name:</b> (obbligatorio) Nome o ID dell'annuncio.</td>
<td>N/D</td>
<td>Non disponibile</td>
</tr>
<tr>
<td>
length
</td>
<td>
<b>lunghezza:</b> (obbligatorio) Lunghezza dell'annuncio.
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Playername
</td>
<td>
<b>Playername:</b> (obbligatorio) Il nome del lettore multimediale utilizzato
per visualizzare l'annuncio.
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Parentname
</td>
<td>
<b>Parentname:</b> Nome o ID del contenuto principale in cui
è incorporato l'annuncio.
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Parentpod
</td>
<td>
<b>Parentpod:</b> La posizione nel contenuto principale in cui è stato riprodotto l'annuncio.
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Parentpodposition
</td>
<td>
<b>Parentpodposition:</b> Posizione all'interno del contenitore in cui viene riprodotto l'annuncio.
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
<b>CPM:</b> CPM o CPM cifrato (prefisso a " ~") che si applica a questa riproduzione.
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media. click
</td>
<td>
<pre>
s. Media. click (nome, offset)
</pre>
</td>
<td>
<pre>
s. tl ()
</pre>
</td>
<td>Utilizzare una chiamata di analisi dei collegamenti personalizzata per tenere traccia dei clic
</td>
</tr>
<tr>
<td>
File multimediali. close
</td>
<td>
<pre>
s. Media. close (medianame)
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
File multimediali. complete
</td>
<td>
<pre>
s. Media. complete (nome,
 offset)
</pre>
</td>
<td>
s. tl ()
</td>
<td>
<pre>
s. linktrackvars
 ='events,
 prop 10,
 evar 10,
 evar 12,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. completè;
s. linktrackevents 
 ='event 3 ';
s. prop 10 
 = Medianame;
s. evar 10 
 = Medianame;
s. evar 12 
 = "video";
s. evar 15 
 = Mediaplayername;
s. events 
 ='event 3 ';
s. contextdata ['video. namè]
 = medianame;
s. contextdata ['video. completè]
 ='truè;
s. tl (this,'o ','Video Completè);
</pre>
</td>
</tr>
<tr>
<td>
Media. play
</td>
<td>
<pre>
s. Media. play (name,
 offset,
 segmentnum,
 segment,
 segmentlength)
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media. stop
</td>
<td>
<pre>
s. Media. stop (medianame,
 mediaoffset)
</pre>
</td>
<td>N/D 
</td>
<td>Non disponibile
</td>
</tr>
<tr>
<td>
Media. monitor
</td>
<td>
<pre>
s. Media. monitor (s, media)
</pre>
</td>
<td>
Imposta variabile di dati evar o di contesto nella chiamata di collegamento
</td>
<td>
<pre>
s. linktrackvars
 ='events,
 prop 10,
 evar 10,
 evar 12,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. view ';
s. linktrackevents ='event 2 ';
</pre>
</td>
</tr>
<tr>
<td>
Media. track
</td>
<td>
<pre>
s. Media. track (medianame)
</pre>
</td>
<td>N/D
</td>
<td>Non disponibile
</td>
</tr>
</tbody>
</table>

