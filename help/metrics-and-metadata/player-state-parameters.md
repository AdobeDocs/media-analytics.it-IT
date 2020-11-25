---
title: Parametri dello stato del lettore
description: Questo argomento descrive i parametri di tracciamento dello stato del lettore.
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 1cf631d7f3d5365a02be99af78655ac3b53fb3cb
workflow-type: tm+mt
source-wordcount: '2236'
ht-degree: 1%

---


# Parametri dello stato del lettore{#player-state-parameters}

Questo argomento presenta un elenco di dati sullo stato del lettore che  Adobe raccoglie tramite variabili della soluzione.

Descrizione dati tabella:

* **Implementazione:** informazioni su valori e requisiti di implementazione
   * *Chiave*  - Variabile, impostata manualmente nell&#39;app o automaticamente dall&#39;SDK per file multimediali del Adobe .
   * *Obbligatorio*  - Indica se il parametro è richiesto per il tracciamento video di base.
   * *Tipo*  - Specifica il tipo di variabile da impostare, stringa o numero.
   * *Inviato con*  - Indica quando i dati vengono inviati:  *Media* Start è la chiamata di analisi inviata all’avvio del supporto,  *Ad* Started è la chiamata di analisi inviata all’avvio dell’annuncio e così via; le  ** chiusure sono le chiamate di analisi compilate inviate direttamente dal server heartbeat al server di analisi alla fine della sessione multimediale, oppure alla fine dell&#39;annuncio, del capitolo e così via. Le chiamate di chiusura non sono disponibili nelle chiamate dei pacchetti di rete.
   * *Min. Versione SDK* - Indica la versione SDK a cui sarà necessario accedere per il parametro.
   * *Valore*  di esempio - Fornisce un esempio di utilizzo comune delle variabili.
* **Parametri di rete:** visualizza i valori passati ai server Adobe Analytics o Heartbeat . Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate da  Adobe Media SDK.
* **Rapporti:** informazioni su come visualizzare e analizzare i dati video.
   * *Disponibile*  - Indica se i dati sono disponibili nel reporting per impostazione predefinita (*Sì*) o richiedono una configurazione personalizzata (*Personalizzato*)
   * *Variabile*  riservata - Indica se i dati vengono acquisiti come evento,  eVar, prop o classificazione in una variabile riservata.
   * *Nome*  report - Nome del report di analisi dei Adobi  per la variabile
   * *Dati*  contestuali - Nome dei dati contestuali  Adobe Analytics passati al server di reporting e utilizzati nelle regole di elaborazione.
   * *Feed*  dati - Nome colonna per la variabile trovata nei feed di dati Clickstream o Live Stream
   * *Audience Manager*   - Nome caratteristica trovato in Adobe Audience Manager

>[!IMPORTANT]
>
>Non modificare i nomi delle classificazioni per le variabili elencate di seguito che sono descritte in Reporting/Riservato Variabile come &quot;classificazione&quot;.\
>Le classificazioni dei supporti vengono definite quando una suite di rapporti è abilitata per il tracciamento dei supporti. Di tanto in tanto,  Adobe aggiunge nuove proprietà e, in questo caso, i clienti devono riabilitare le suite di rapporti per accedere alle nuove proprietà del supporto. Durante il processo di aggiornamento  Adobe determina se le classificazioni sono abilitate controllando i nomi delle variabili. Se manca qualcuno di loro,  Adobe aggiunge di nuovo quelli mancanti.

## Proprietà stato lettore {#player-state-properties}

Le funzionalità di tracciamento dello stato del lettore possono essere collegate a un flusso audio o video. Le metriche standard di tracciamento dello stato del lettore sono memorizzate come variabili della soluzione. Gli stati standard sono: fullScreen, mute, closeCaption, pictureInPicture e inFocus.

### Proprietà a schermo intero

#### Streams interessati dallo schermo intero

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeySet automatico  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min. Versione SDK**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> Descrizione: il numero di flussi interessati dallo schermo intero. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato a schermo intero. <br/> **** <br/> Importante: se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.fullscreen.set<br/></li> <li> **HeartbeatN/D**<br/>  </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Evento**<br/> Variabile Riservato </li> <li> **Report**<br/> NameStreams interessati dallo schermo intero </li> <li> **Dati**<br/> contestuali.media.States.fullscreen.set<br/> </li> <li> **Data**<br/> Feedvideostatefullscreen </li> <li> **Audience**<br/> Manager_contextdata.a.media.States.fullscreen.set </li> </ul> |

#### Conteggi a schermo intero

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeySet automatico  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min. Versione SDK**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> Descrizione: il numero di volte in cui è stato visualizzato uno schermo intero. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato a schermo intero. <br/> ****<br/> Importante: se questo evento è impostato, il conteggio è uguale al numero di volte in cui il video era nello stato Schermo intero. Se questo evento non è impostato, non viene inviato alcun valore.</li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.fullscreen.count<br/></li> <li> **HeartbeatN/D**<br/>  </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Evento**<br/> Variabile Riservato </li> <li> **Conteggio**<br/> nome rapporto a schermo intero </li> <li> **Dati**<br/> contestuali.media.States.fullscreen.count<br/> </li> <li> **Data**<br/> Feedvideostatefullscreencount </li> <li> **Audience**<br/> Manager_contextdata.media.States.fullscreen.count </li> </ul> |



#### Durata totale schermo intero

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeySet automatico  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min. Versione SDK**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> Descrizione: la durata di visualizzazione di uno schermo intero. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato a schermo intero. <br/> ****<br/>  Importante: se questo evento è impostato, l’ora è uguale a quanto tempo il video era nello stato Schermo intero. Se questo evento non è impostato, non viene inviato alcun valore.  </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.fullscreen.time<br/></li> <li> **HeartbeatN/D**<br/>  </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Evento**<br/> Variabile Riservato </li> <li> **Durata totale**<br/> nome rapportoSchermo intero </li> <li> **Dati**<br/> contestuali.media.States.fullscreen.time<br/> </li> <li> **Data**<br/> Feedvideostatefullscreentime </li> <li> **Audience**<br/> Manager_contextdata.media.States.fullscreen.time </li> </ul> |


### Chiudi proprietà didascalia

#### Streams interessati dai sottotitoli

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeySet automatico  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min. Versione SDK**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> Descrizione: il numero di flussi interessati dai sottotitoli. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato dei sottotitoli codificati. <br/> **** <br/>  Importante: se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.closedcaptioning.set<br/></li> <li> **HeartbeatN/D**<br/>  </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Evento**<br/> Variabile Riservato </li> <li> **Report**<br/> NameStreams interessati dai sottotitoli </li> <li> **Context**<br/> Data.media.States.closedcaptioning.set<br/> </li> <li> **Data**<br/> Feedvideostateclosedcaptioning </li> <li> **Audience**<br/> Manager_contextdata.a.media.States.closedcaptioning.set </li> </ul> |


#### Conteggi sottotitoli codificati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeySet automatico  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min. Versione SDK**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> Descrizione: il numero di volte in cui sono stati visualizzati i sottotitoli codificati. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato di sottotitoli codificati. <br/> ****<br/>  Importante: se questo evento è impostato, il conteggio è uguale al numero di volte in cui il video si trovava nello stato Sottotitoli codificati. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.closedcaptioning.count<br/></li> <li> **HeartbeatN/D**<br/>  </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Evento**<br/> Variabile Riservato </li> <li> **Numero**<br/> di sottotitoli codificati </li> <li> **Contesto**<br/> Dati.media.stati.closedcaptioning.count<br/> </li> <li> **Data**<br/> Feedvideostateclosedcaptioningcount </li> <li> **Audience**<br/> Manager_contextdata.media.States.closedcaptioning.count </li> </ul> |


#### Durata totale sottotitoli

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeySet automatico  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min. Versione SDK**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> Descrizione: il tempo di visualizzazione dei sottotitoli codificati. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato a schermo intero. <br/> ****<br/>  Importante: se questo evento è impostato, l’ora corrisponde a quanto tempo il video si trovava nello stato Sottotitoli codificati. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.closedcaptioning.time<br/></li> <li> **HeartbeatN/D**<br/>  </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Evento**<br/> Variabile Riservato </li> <li> **Nome reportDurata totale sottotitoli**<br/> chiusi </li> <li> **Dati**<br/> contestuali.media.States.closedcaptioning.time<br/> </li> <li> **Data**<br/> Feedvideostateclosedcaptioningtime </li> <li> **Audience**<br/> Manager_contextdata.media.States.closedcaptioning.time </li> </ul> |


### Disattiva proprietà

#### Streams interessati dall&#39;audio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeySet automatico  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min. Versione SDK**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> Descrizione: il numero di flussi interessati dall&#39;audio. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato di disattivazione audio. <br/> **** <br/> Importante: se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.mute.set<br/></li> <li> **HeartbeatN/D**<br/>  </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Evento**<br/> Variabile Riservato </li> <li> **Report**<br/> NameStreams interessati dall&#39;attivazione </li> <li> **Context**<br/> Data.media.States.mute.set<br/> </li> <li> **Data**<br/> Feedvideo: disattivazione </li> <li> **Audience**<br/> Manager_contextdata.a.media.States.mute.set </li> </ul> |

#### Disattiva conteggio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeySet automatico  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min. Versione SDK**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> Descrizione: il numero di volte in cui è stato visualizzato Disattiva audio. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato di disattivazione audio. <br/> ****<br/>  Importante: se questo evento è impostato, il conteggio è uguale al numero di volte in cui il video è stato disattivato. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.mute.count<br/></li> <li> **HeartbeatN/D**<br/>  </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Evento**<br/> Variabile Riservato </li> <li> **Conteggio**<br/> audio nome rapporto </li> <li> **Context**<br/> Data.media.States.mute.count<br/> </li> <li> **Data**<br/> Feedvideostatemutecount </li> <li> **Audience**<br/> Manager_contextdata.media.States.mute.count </li> </ul> |

#### Disattiva durata totale

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeySet automatico  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min. Versione SDK**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> Descrizione: il tempo di disattivazione dell&#39;audio è stato visualizzato. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato di disattivazione audio. <br/> ****<br/> Importante: se questo evento è impostato, l’ora è uguale a quanto tempo il video è stato disattivato. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.mute.time<br/></li> <li> **HeartbeatN/D**<br/>  </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Evento**<br/> Variabile Riservato </li> <li> **Durata totale**<br/> nome rapportoDisattiva audio </li> <li> **Dati**<br/> di contesto.media.state.mute.time<br/> </li> <li> **Data**<br/> Feedvideostatemutetime </li> <li> **Audience**<br/> Manager_contextdata.media.States.mute.time </li> </ul> |


### Proprietà immagine


#### Streams interessati da Picture in Picture

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeySet automatico  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min. Versione SDK**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> Descrizione: il numero di flussi interessati da Picture in Picture. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato Picture in Picture. <br/> **** <br/> Importante: se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.pictureinpicture.set<br/></li> <li> **HeartbeatN/D**<br/>  </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Evento**<br/> Variabile Riservato </li> <li> **Report**<br/> NameStreams interessati da Picture in Picture </li> <li> **Context**<br/> Data.media.States.pictureinpicture.set<br/> </li> <li> **Data**<br/> Feedvideostatepictureinpicture </li> <li> **Audience**<br/> Manager_contextdata.a.media.States.pictureinpicture.set </li> </ul> |


#### Conteggio immagini

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeySet automatico  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min. Versione SDK**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> Descrizione: il numero di volte in cui è stato visualizzato Picture in Picture. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato Picture in Picture. <br/> **** <br/> Importante: se questo evento è impostato, il conteggio è uguale al numero di volte in cui il video si trovava nello stato Picture in Picture. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.pictureinpicture.count<br/></li> <li> **HeartbeatN/D**<br/>  </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Evento**<br/> Variabile Riservato </li> <li> **Report**<br/> NamePicture in Picture Count </li> <li> **Context**<br/> Data.media.States.pictureinpicture.count<br/> </li> <li> **Data**<br/> Feedvideostatepicturepicturecount </li> <li> **Audience**<br/> Manager_contextdata.media.States.pictureinpicture.count </li> </ul> |


#### Durata totale immagine

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeySet automatico  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min. Versione SDK**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> DescrizioneDurata della visualizzazione Immagine nell&#39;immagine. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato Picture in Picture. <br/> **** <br/> Importante: se questo evento è impostato, l’ora è uguale a quanto tempo il video era nello stato Picture in Picture. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.pictureinpicture.time<br/></li> <li> **HeartbeatN/D**<br/>  </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Evento**<br/> Variabile Riservato </li> <li> **Nome rapportoDurata totale immagine**<br/> immagine </li> <li> **Dati**<br/> contestuali.media.States.pictureinpicture.time<br/> </li> <li> **Data**<br/> Feedvideostatepictureinpitretime </li> <li> **Audience**<br/> Manager_contextdata.media.States.pictureinpicture.time </li> </ul> |


### Proprietà dello stato attivo

#### Streams interessati da In Focus

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeySet automatico  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min. Versione SDK**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> Descrizione: il numero di flussi interessati da In Focus. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato attivo. <br/> **** <br/> Importante: se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.infocus.set<br/></li> <li> **HeartbeatN/D**<br/>  </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Evento**<br/> Variabile Riservato </li> <li> **Report**<br/> NameStreams interessati da In Focus </li> <li> **Dati**<br/> contestuali.media.States.infocus.set<br/> </li> <li> **Data**<br/> Feedvideostateinfocus </li> <li> **Audience**<br/> Manager_contextdata.a.media.States.infocus.set </li> </ul> |


#### Conteggi per area di interesse

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeySet automatico  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min. Versione SDK**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> Descrizione: il numero di volte in cui è stato visualizzato In stato attivo. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato attivo. <br/> ****<br/>  Importante: se questo evento è impostato, il conteggio è uguale al numero di volte in cui il video si trovava nello stato Attivo. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.infocus.count<br/></li> <li> **HeartbeatN/D**<br/>  </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Evento**<br/> Variabile Riservato </li> <li> **Conteggio**<br/> nome report in stato attivo </li> <li> **Dati**<br/> contestuali.media.States.infocus.count<br/> </li> <li> **Data**<br/> Feedvideostateinfocuscount </li> <li> **Audience**<br/> Manager_contextdata.media.States.infocus.count </li> </ul> |


#### Durata totale messa a fuoco

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **SDK**<br/> KeySet automatico  </li> <li> **API**<br/> KeyN/D </li> <li> ****<br/> RequiredNo </li> <li> ****<br/> Typenumber </li> <li> **Inviato**<br/> con Media Close </li> <li> **Min. Versione SDK**<br/> 3.0</li> <li> **Sample**<br/> ValueTRUE </li><li> ****<br/> Descrizione: il tempo di attivazione visualizzato. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato attivo. <br/> **** <br/> Importante: se questo evento è impostato, l’ora è uguale a quanto tempo il video è stato nello stato Attivo. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe**<br/> Analytics.media.States.infocus.time<br/></li> <li> **HeartbeatN/D**<br/>  </li> </ul> | <ul> <li> ****<br/> AvailableYes </li> <li> **Evento**<br/> Variabile Riservato </li> <li> **Durata totale**<br/> nome report in stato attivo </li> <li> **Dati**<br/> contestuali.media.States.infocus.time<br/> </li> <li> **Data**<br/> Feedvideostateinfocustime </li> <li> **Audience**<br/> Manager_contextdata.media.States.infocus.time </li> </ul> |

## Elenco delle proprietà per le identità XDM

I dati memorizzati in Analytics possono essere utilizzati per qualsiasi scopo e le metriche relative allo stato del lettore possono essere importate in Adobe Experience Platform utilizzando XDM e utilizzate con Customer Journey Analytics.

| Proprietà stato lettore | Mapping |
|---------------------------------------|------------------------------------|
| a.media.states.fullScreen.set | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateSet |
| a.media.states.fullScreen.count | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateCount |
| a.media.states.fullScreen.time | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateTime |
| a.media.states.mute.set | media.mediaTimed.primaryAssetViewDetails.mute.playerStateSet |
| a.media.states.mute.count | media.mediaTimed.primaryAssetViewDetails.mute.playerStateCount |
| a.media.states.mute.time | media.mediaTimed.primaryAssetViewDetails.mute.playerStateTime |
| a.media.states.closeCaption.set | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateSet |
| a.media.states.closeCaption.count | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateCount |
| a.media.states.closeCaption.time | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateTime |
| a.media.states.pictureInPicture.set | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateSet |
| a.media.states.pictureInPicture.count | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateCount |
| a.media.states.pictureInPicture.time | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateTime |
| a.media.states.inFocus.set | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateSet |
| a.media.states.inFocus.count | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateCount |
| a.media.states.inFocus.time | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateTime |

## API correlate {#related_apis_section}

* Android - [createStateObject](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* iOS - [createStateObjectWithName](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* Javascript - [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)
