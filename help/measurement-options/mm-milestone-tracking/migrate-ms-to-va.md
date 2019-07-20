---
seo-title: Migrazione da Milestone a Media Analytics
title: Migrazione da Milestone a Media Analytics
uuid: fdc 96146-af 63-48 ce-b 938-c 0 ca 70729277
translation-type: tm+mt
source-git-commit: 27740fc1753e8ac9cf5a4b240a56b1c2dd567010

---


# Migrating from Milestone to Media Analytics {#migrating-from-milestone-to-media-analytics}

## Panoramica {#section_ihl_nbz_cfb}

I concetti principali della misurazione video sono identici per Milestone and Media Analytics (Pietra miliare e Media Analytics), che occupano eventi del lettore video e li mappano sui metodi di analisi, e li mappano anche sui metadati e i valori del lettore e mappatura sulle variabili di analisi. La soluzione Media Analytics è cresciuta da Milestone, molti dei metodi e delle metriche sono la stessa, tuttavia, l'approccio di configurazione e il codice sono cambiati in modo significativo. Dovrebbe essere possibile aggiornare il codice dell'evento del lettore in modo che faccia riferimento ai nuovi metodi di Media Analytics. See [SDK Overview](../../sdk-implement/setup/setup-overview.md) and [Tracking Overview](../../sdk-implement/track-av-playback/track-core-overview.md) for more details on implementing Media Analytics.

Le tabelle seguenti forniscono traduzioni tra la soluzione Milestone (Pietra miliare) e la soluzione Media Analytics.

## Migration guide {#section_iyb_pbz_cfb}

### Riferimento variabile

| Milestone Metric (Metrica milestone Metrica) | Tipo di variabile | Metrica Media Analytics |
| --- | --- | --- |
| Contenuto | eVar<br/><br/>Default expiration: Visit | Contenuto |
| Tipo di contenuto | eVar<br/><br/> Default expiration: Page view | Tipo di contenuto |
| Tempo contenuto trascorso | Event<br/><br/> Type: Counter | Tempo contenuto trascorso |
| Video avviato | Event<br/><br/> Type: Counter | Video avviato |
| Completamenti video | Event<br/><br/> Type: Counter | Completamento contenuto |

### Variabili modulo Media

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintassi milestone (Pietra miliare)
</th>
<th>Media Analytics
</th>
<th>Sintassi Media Analytics
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
s. Media. trackusingcontextdata
 = true;
</pre>
</td>
<td>N/D
</td>
<td>Tutti i dati di Media Analytics vengono inviati solo utilizzando i dati contestuali.
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
<td>I dati contestuali di Media Analytics vengono compilati automaticamente in
variabili riservate. Mappatura su evar, prop ed eventi non più necessaria all'interno del codice di implementazione. I clienti possono mappare i dati contestuali
alle variabili utilizzando le regole di elaborazione.
</td>
</tr>
<tr>
<td>
Media. trackvars
</td>
<td>
<pre>
s. Media. trackvars = 
 " events,
 prop 2,
 evar 1,
 evar 2,
 evar 3 ";
</pre>
</td>
<td>N/D
</td>
<td>Non è più necessario perché la mappatura avviene tramite variabili riservate e
regole di elaborazione.
</td>
</tr>
<tr>
<td>
Media. trackevents
</td>
<td>
<pre>
s. Media. trackevents = 
 " event 1,
 event 2,
 event 3,
 event 4,
 event 5,
 event 6,
 event 7 "
</pre>
</td>
<td>N/D
</td>
<td>Non è più necessario perché la mappatura avviene tramite variabili riservate e
regole di elaborazione.
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
<th>Media Analytics
</th>
<th>Sintassi Media Analytics
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
<td>Non forniamo più mappature del lettore pre-costruite.
</td>
</tr>
<tr>
<td>
Media. autotracknetstreams
</td>
<td>
<pre>
s. Media.
 Autotracknetstreams
 = true
</pre>
</td>
<td>N/D
</td>
<td>Non forniamo più mappature del lettore pre-costruite.
</td>
</tr>
<tr>
<td>
Media. completebycloseoffset
</td>
<td>
<pre>
s. Media.
 Completebycloseoffset
 = true
</pre>
</td>
<td>N/D
</td>
<td>Contenuto completato supporta solo un marcatore di avanzamento 100%.
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
<td>Contenuto completato supporta solo un marcatore di avanzamento 100%.
</td>
</tr>
<tr>
<td>
Media. playername
</td>
<td>
<pre>
s. Media. playername
 = "Custom Player Name"
</pre>
</td>
<td>
Chiave SDK: Playername; 
Chiave API: media. playername
</td>
<td>
<pre>
Mediaheartbeatconfig.
 Playername
</pre>
</p>
</td>
</tr>
<tr>
<td>
Media. trackseconds
</td>
<td>
<pre>
s. Media.
 Trackseconds
 = 15
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics è impostato su 10 secondi per il contenuto e su 1 secondo per
gli annunci. Non sono disponibili altre opzioni.
</td>
</tr>
<tr>
<td>
Media. trackmilestones
</td>
<td>
<pre>
s. Media.
 Trackmilestones
 = "25,50,75";
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics tiene traccia sempre dei marcatori di avanzamento al 10%, 25%, 50%,
75%, 95%
</td>
</tr>
<tr>
<td>
Media. trackoffsetmilestones
</td>
<td>
<pre>
s. Media.
 Trackoffsetmilestones
 = "20,40,60";
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics tiene traccia sempre dei marcatori di avanzamento al 10%, 25%, 50%,
75%, 95%
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
<td>La traccia automatica non è più disponibile
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
<th>Sintassi milestone (Pietra miliare)
</th>
<th>Media Analytics
</th>
<th>Sintassi Media Analytics
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
s. Media.
 Adtrackseconds
 = 15
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics è impostato su 10 secondi per il contenuto e su 1 secondo per
gli annunci. Non sono disponibili altre opzioni.
</td>
</tr>
<tr>
<td>
Media. adtrackmilestones
</td>
<td>
<pre>
s. Media.
 Adtrackmilestones
 = "25,50,75";
</pre>
</td>
<td>N/D
</td>
<td>I marcatori di progresso non sono forniti per impostazione predefinita per gli annunci. Utilizzate
le metriche calcolate per creare marcatori di avanzamento annunci.
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
<td>Media Analytics è impostato su 1 secondo per gli annunci. Non sono disponibili altre opzioni.
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
<td>La traccia automatica non è più disponibile
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
<td>La traccia automatica non è più disponibile
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
<th>Media Analytics
</th>
<th>Sintassi Media Analytics
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
File multimediali. open
</td>
<td>
<pre>
s. Media. open (medianame,
 medialength,
 mediaplayername)
</pre>
</td>
<td>
<pre>
Tracksessionstart
</pre>
</td>
<td>
<pre>
Tracksessionstart (mediaobject, 
 Contextdata)
</pre>
</td>
</tr>
<tr>
<td>
Medianame - (obbligatorio) Il nome del video che viene
visualizzato nei rapporti video.
</td>
<td>
<pre>
Medianame
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
Createmediaobject (name, 
 Mediaid, 
 length, 
 Streamtype)
</pre>
</td>
</tr>
<tr>
<td>
Medialength - (obbligatorio) La lunghezza del video
in secondi.
</td>
<td>
<pre>
Medialength
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
Createmediaobject (name, 
 Mediaid, 
 length, 
 Streamtype)
</pre>
</td>
</tr>
<tr>
<td>
Mediaplayername - (obbligatorio) Il nome del lettore multimediale utilizzato per visualizzare il video, in modo che venga visualizzato nei rapporti video.
</td>
<td>
<pre>
Mediaplayername
</pre>
</td>
<td>
<pre>
Playername
</pre>
</td>
<td>
<pre>
Mediaheartbeatconfig.
 Playername
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
<td>
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
Mediaheartbeat. trackevent (mediaheartbeat.
 Evento.
    Adbreakstart, 
 Adbreakobject);
…
Trackevent (mediaheartbeat.
 Evento.
    Adstart, 
 Adobject, 
 Adcustommetadata);
</pre>
</td>
</tr>
<tr>
<td>
name - (obbligatorio) Il nome o l'ID dell'annuncio.
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
Createadobject (nome, 
 Adid, 
 position, 
 length)
</pre>
</td>
</tr>
<tr>
<td>
length
(obbligatorio) Lunghezza dell'annuncio.
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
Createadobject (nome, 
 Adid, 
 position, 
 length)
</pre>
</td>
</tr>
<tr>
<td>
Playername - (obbligatorio) Il nome del lettore multimediale
utilizzato per visualizzare l'annuncio.
</td>
<td>
<pre>
Playername
</pre>
</td>
<td>
<pre>
Playername
</pre>
</td>
<td>
<pre>
Mediaheartbeatconfig.
 Playername
</pre>
</td>
</tr>
<tr>
<td>
Parentname: nome o ID del contenuto principale in cui è incorporato l'annuncio.
</td>
<td>
<pre>
Parentname
</pre>
</td>
<td>N/D
</td>
<td>Ereditata automaticamente
</td>
</tr>
<tr>
<td>
Parentpod: posizione nel contenuto principale in cui è stato riprodotto l'annuncio.
</td>
<td>
<pre>
Parentpod
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
Createadbreakobject (name, 
 position, 
 Starttime
</pre>
</td>
</tr>
<tr>
<td>
Parentpodposition - Posizione all'interno del contenitore in cui viene riprodotta l'annuncio.
</td>
<td>
<pre>
Parentpodposition
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
Createadobject (nome, 
 Adid, 
 position, 
 length)
</pre>
</td>
</tr>
<tr>
<td>
CPM:
CPM o CPM cifrato (prefisso a " ~") che si applica a questa riproduzione.
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
Media. click
</td>
<td>
<pre>
s. Media. click (nome,
 offset)
</pre>
</td>
<td>N/D
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
<td>
<pre>
Tracksessionend
</pre>
</td>
<td>
<pre>
Tracksessionend ()
</pre>
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
<pre>
Trackcomplete
</pre>
</td>
<td>
<pre>
Trackcomplete ()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media. play
</pre>
</td>
<td>
<pre>
s. Media. play (nome,
 offset,
 segmentnum,
 segmento, 
 Segmentlength
</pre>
</td>
<td>
<pre>
Trackplay
</pre>
</td>
<td>
<pre>
Trackplay ()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media. stop
</pre>
</td>
<td>
<pre>
s. Media. stop (medianame,
 mediaoffset)
</pre>
</td>
<td>
<pre>
Trackpause
</pre>  oppure  
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
Trackpause ()
</pre> 
 oppure 
<pre>
Trackevent (mediaheartbeat.
 Evento.
  Seekstart
</pre>  oppure 
<pre>
Trackevent (mediaheartbeat.
 Evento.
  Bufferstart);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media. monitor
</pre>
</td>
<td>
<pre>
s. Media. monitor (s, media)
</pre>
</td>
<td>Utilizzare metadati personalizzati o standard per impostare ulteriori variabili
</td>
<td>
<pre>
var customvideometadata = 
{isuserloggedin: 
 " false ",
 tvstation: 
 " Sample TV station ",
 programer: 
 " Sample programer "};
…
var standardvideometadata 
 = {};
Standardvideometadata
 [mediaheartbeat.
 Videometadatakeys.
 EPISODE] = 
 " Sample Episode ";
Standardvideometadata
 [mediaheartbeat.
 Videometadatakeys.
 SHOW] = "Sample Show";
…
Mediaobject. setvalue (mediaheartbeat.
 Mediaobjectkey.
 Standardvideometadata, 
 Standardvideometadata);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media. track
</pre>
</td>
<td>
<pre>
s. Media. track (medianame)
</pre>
</td>
<td>N/D
</td>
<td>La frequenza di chiamata di tracciamento viene impostata automaticamente.
</td>
</tr>
</tbody>
</table>

