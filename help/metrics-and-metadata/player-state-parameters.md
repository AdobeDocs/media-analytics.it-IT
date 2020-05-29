---
title: Parametri dello stato del lettore
description: Questo argomento descrive i parametri di tracciamento dello stato del lettore.
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: c23a8787a8f59746665702eb5e2e74dde2c213e8
workflow-type: tm+mt
source-wordcount: '2167'
ht-degree: 1%

---


# Parametri dello stato del lettore{#player-state-parameters}

Questo argomento presenta un elenco dei dati sullo stato del lettore raccolti da Adobe tramite le variabili della soluzione.

Descrizione dati tabella:

* **Implementazione:** Informazioni su valori e requisiti di implementazione
   * *Chiave* - Variabile, impostata manualmente nell’app o automaticamente dall’SDK di Adobe Media.
   * *Obbligatorio* - Indica se il parametro è richiesto per il tracciamento video di base.
   * *Tipo* - Specifica il tipo di variabile da impostare, stringa o numero.
   * *Inviato con* - Indica quando i dati vengono inviati: *Media Start* è la chiamata di analisi inviata all’avvio del supporto, *Ad Start* è la chiamata di analisi inviata all’avvio dell’annuncio e così via; le chiamate *Close* sono le chiamate di analisi compilate inviate direttamente dal server Heartbeat al server di analisi alla fine della sessione multimediale, o la fine dell&#39;annuncio, del capitolo, ecc. Le chiamate di chiusura non sono disponibili nelle chiamate dei pacchetti di rete.
   * *Min. Versione* SDK - Indica la versione SDK a cui sarà necessario accedere per il parametro.
   * *Valore* di esempio - Fornisce un esempio di utilizzo comune delle variabili.
* **Parametri di rete:** Visualizza i valori passati ai server Adobe Analytics o Heartbeat. Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate dagli SDK di Adobe Media.
* **Reporting:** Informazioni su come visualizzare e analizzare i dati video.
   * *Disponibile* - Indica se i dati sono disponibili nel reporting per impostazione predefinita (*Sì*) o richiedono una configurazione personalizzata (*Personalizzato*)
   * *Variabile* riservata - Indica se i dati vengono acquisiti come evento, eVar, prop o classificazione in una variabile riservata.
   * *Nome* report - Nome del report Adobe Analytics per la variabile
   * *Dati* contestuali - Nome dei dati contestuali di Adobe Analytics passati al server di reporting e utilizzati nelle regole di elaborazione.
   * *Feed* dati - Nome colonna per la variabile trovata nei feed di dati Clickstream o Live Stream
   * *Audience Manager* - Nome caratteristica trovato in Adobe Audience Manager

>[!IMPORTANT]
>
>Non modificare i nomi delle classificazioni per le variabili elencate di seguito che sono descritte in Reporting/Riservato Variabile come &quot;classificazione&quot;.\
>Le classificazioni dei supporti vengono definite quando una suite di rapporti è abilitata per il tracciamento dei supporti. Di tanto in tanto, Adobe aggiunge nuove proprietà e, in questo caso, i clienti devono riabilitare le suite di rapporti per poter accedere alle nuove proprietà del supporto. Durante il processo di aggiornamento, Adobe determina se le classificazioni sono abilitate controllando i nomi delle variabili. Se manca qualcuno di essi, Adobe aggiunge di nuovo quelli mancanti.

## Proprietà stato lettore {#player-state-properties}

Le funzionalità di tracciamento dello stato del lettore possono essere collegate a un flusso audio o video. Le metriche standard di tracciamento dello stato del lettore sono memorizzate come variabili della soluzione. Gli stati standard sono: fullScreen, mute, closeCaption, pictureInPicture e inFocus.

### Proprietà a schermo intero

#### Streams interessati dallo schermo intero

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave **<br/>SDK impostata automaticamente</li> <li> **Chiave **<br/>API N/D</li> <li> **Numero richiesto **<br/></li> <li> **Numero tipo **<br/></li> <li> **Inviato con **<br/>chiusura file multimediali</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Valore **<br/>campione TRUE</li><li> ****<br/>Descrizione: il numero di flussi interessati dallo schermo intero. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato a schermo intero.<br/> **Importante** <br/> Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.States.fullscreen.set)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponibile **<br/>Sì</li> <li> **Evento variabile **<br/>riservata</li> <li> **Streams Nome **<br/>report interessati dallo schermo intero</li> <li> **Dati **<br/>contestuali (a.media.States.fullscreen.set)<br/> </li> <li> **Feed **<br/>dati media.States.fullscreen</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.States.fullscreen.set)</li> </ul> |

#### Conteggi a schermo intero

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave **<br/>SDK impostata automaticamente</li> <li> **Chiave **<br/>API N/D</li> <li> **Numero richiesto **<br/></li> <li> **Numero tipo **<br/></li> <li> **Inviato con **<br/>chiusura file multimediali</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Valore **<br/>campione TRUE</li><li> ****<br/>Descrizione: il numero di volte in cui è stato visualizzato uno schermo intero. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato a schermo intero.<br/> **Importante **<br/>Se questo evento è impostato, il conteggio è uguale al numero di volte in cui il video era nello stato Schermo intero. Se questo evento non è impostato, non viene inviato alcun valore.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.stati.fullscreen.count)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponibile **<br/>Sì</li> <li> **Evento variabile **<br/>riservata</li> <li> **Conteggio schermo intero nome **<br/>rapporto</li> <li> **Dati **<br/>contestuali (media.stati.fullscreen.count)<br/> </li> <li> **Feed **<br/>dati media.stati.fullscreen.count</li> <li> **Audience Manager **<br/>(c_contextdata.media.States.fullscreen.count)</li> </ul> |



#### Durata totale schermo intero

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave **<br/>SDK impostata automaticamente</li> <li> **Chiave **<br/>API N/D</li> <li> **Numero richiesto **<br/></li> <li> **Numero tipo **<br/></li> <li> **Inviato con **<br/>chiusura file multimediali</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Valore **<br/>campione TRUE</li><li> ****<br/>Descrizione: la durata di visualizzazione di uno schermo intero. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato a schermo intero.<br/> **Importante **<br/>Se questo evento è impostato, l’ora è uguale a quanto tempo il video era nello stato Schermo intero. Se questo evento non è impostato, non viene inviato alcun valore.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.stati.fullscreen.time)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponibile **<br/>Sì</li> <li> **Evento variabile **<br/>riservata</li> <li> **Nome **<br/>rapporto - Durata totale schermo</li> <li> **Dati **<br/>contestuali (media.stati.fullscreen.time)<br/> </li> <li> **Feed **<br/>dati media.States.fullscreen.time</li> <li> **Audience Manager **<br/>(c_contextdata.media.States.fullscreen.time)</li> </ul> |


### Chiudi proprietà didascalia

#### Streams interessati dai sottotitoli

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave **<br/>SDK impostata automaticamente</li> <li> **Chiave **<br/>API N/D</li> <li> **Numero richiesto **<br/></li> <li> **Numero tipo **<br/></li> <li> **Inviato con **<br/>chiusura file multimediali</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Valore **<br/>campione TRUE</li><li> ****<br/>Descrizione: il numero di flussi interessati dai sottotitoli. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato dei sottotitoli codificati.<br/> **Importante** <br/> Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.States.closedcaptioning.set)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponibile **<br/>Sì</li> <li> **Evento variabile **<br/>riservata</li> <li> **Streams dei nomi **<br/>dei report interessati dai sottotitoli</li> <li> **Dati **<br/>contestuali (a.media.States.closedcaptioning.set)<br/> </li> <li> **Feed **<br/>dati media.stati.closedcaptioning</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.States.closedcaptioning.set)</li> </ul> |


#### Conteggi sottotitoli codificati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave **<br/>SDK impostata automaticamente</li> <li> **Chiave **<br/>API N/D</li> <li> **Numero richiesto **<br/></li> <li> **Numero tipo **<br/></li> <li> **Inviato con **<br/>chiusura file multimediali</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Valore **<br/>campione TRUE</li><li> ****<br/>Descrizione: il numero di volte in cui sono stati visualizzati i sottotitoli codificati. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato di sottotitoli codificati.<br/> **Importante **<br/>Se questo evento è impostato, il conteggio è uguale al numero di volte in cui il video si trovava nello stato Sottotitoli codificati. Se questo evento non è impostato, non viene inviato alcun valore.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(C19)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponibile **<br/>Sì</li> <li> **Evento variabile **<br/>riservata</li> <li> **Conteggio sottotitoli **<br/>chiusi per nome rapporto</li> <li> **Dati **<br/>contestuali (media.States.closedcaptioning.count)<br/> </li> <li> **Feed **<br/>dati media.States.closedcaptioning.count</li> <li> **Audience Manager **<br/>(c_contextdata.media.States.closedcaptioning.count)</li> </ul> |


#### Durata totale sottotitoli

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave **<br/>SDK impostata automaticamente</li> <li> **Chiave **<br/>API N/D</li> <li> **Numero richiesto **<br/></li> <li> **Numero tipo **<br/></li> <li> **Inviato con **<br/>chiusura file multimediali</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Valore **<br/>campione TRUE</li><li> ****<br/>Descrizione: il tempo di visualizzazione dei sottotitoli codificati. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato a schermo intero.<br/> **Importante **<br/>Se questo evento è impostato, l’ora è uguale a quanto tempo il video si trovava nello stato Sottotitoli codificati. Se questo evento non è impostato, non viene inviato alcun valore.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.stati.closedcaptioning.time)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponibile **<br/>Sì</li> <li> **Evento variabile **<br/>riservata</li> <li> **Nome **<br/>report Sottotitoli codificati Durata totale</li> <li> **Dati **<br/>contestuali (media.state.closedcaptioning.time)<br/> </li> <li> **Feed **<br/>dati media.States.closedcaptioning.time</li> <li> **Audience Manager **<br/>(c_contextdata.media.States.closedcaptioning.time)</li> </ul> |


### Disattiva proprietà

#### Streams interessati dall&#39;audio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave **<br/>SDK impostata automaticamente</li> <li> **Chiave **<br/>API N/D</li> <li> **Numero richiesto **<br/></li> <li> **Numero tipo **<br/></li> <li> **Inviato con **<br/>chiusura file multimediali</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Valore **<br/>campione TRUE</li><li> ****<br/>Descrizione: il numero di flussi interessati dall&#39;audio. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato di disattivazione audio.<br/> **Importante** <br/> Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.States.mute.set)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponibile **<br/>Sì</li> <li> **Evento variabile **<br/>riservata</li> <li> **Streams dei nomi **<br/>dei report interessati dall&#39;audio</li> <li> **Dati **<br/>contestuali (a.media.States.mute.set)<br/> </li> <li> **Feed **<br/>dati media.States.mute</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.States.mute.set)</li> </ul> |

#### Disattiva conteggio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave **<br/>SDK impostata automaticamente</li> <li> **Chiave **<br/>API N/D</li> <li> **Numero richiesto **<br/></li> <li> **Numero tipo **<br/></li> <li> **Inviato con **<br/>chiusura file multimediali</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Valore **<br/>campione TRUE</li><li> ****<br/>Descrizione: il numero di volte in cui è stato visualizzato Disattiva audio. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato di disattivazione audio.<br/> **Importante **<br/>Se questo evento è impostato, il conteggio è uguale al numero di volte in cui il video è stato disattivato. Se questo evento non è impostato, non viene inviato alcun valore.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.stati.mute.count)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponibile **<br/>Sì</li> <li> **Evento variabile **<br/>riservata</li> <li> **Conteggio disattivazione nome **<br/>rapporto</li> <li> **Dati **<br/>contestuali (media.state.mute.count)<br/> </li> <li> **Feed **<br/>dati media.stati.mute.count</li> <li> **Audience Manager **<br/>(c_contextdata.media.States.mute.count)</li> </ul> |

#### Disattiva durata totale

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave **<br/>SDK impostata automaticamente</li> <li> **Chiave **<br/>API N/D</li> <li> **Numero richiesto **<br/></li> <li> **Numero tipo **<br/></li> <li> **Inviato con **<br/>chiusura file multimediali</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Valore **<br/>campione TRUE</li><li> ****<br/>Descrizione: il tempo di disattivazione dell&#39;audio è stato visualizzato. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato di disattivazione audio.<br/> **Importante **<br/>Se questo evento è impostato, l’ora è uguale a quanto tempo il video è stato disattivato. Se questo evento non è impostato, non viene inviato alcun valore.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.state.mute.time)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponibile **<br/>Sì</li> <li> **Evento variabile **<br/>riservata</li> <li> **Nome **<br/>rapporto Disattiva audio - Durata totale</li> <li> **Dati **<br/>contestuali (media.state.mute.time)<br/> </li> <li> **Feed **<br/>dati media.States.mute.time</li> <li> **Audience Manager **<br/>(c_contextdata.media.state.mute.time)</li> </ul> |


### Proprietà immagine


#### Streams interessati da Picture in Picture

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave **<br/>SDK impostata automaticamente</li> <li> **Chiave **<br/>API N/D</li> <li> **Numero richiesto **<br/></li> <li> **Numero tipo **<br/></li> <li> **Inviato con **<br/>chiusura file multimediali</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Valore **<br/>campione TRUE</li><li> ****<br/>Descrizione: il numero di flussi interessati da Picture in Picture. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato Picture in Picture.<br/> **Importante** <br/> Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.States.pictureinpicture.set)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponibile **<br/>Sì</li> <li> **Evento variabile **<br/>riservata</li> <li> **Streams dei nomi **<br/>dei report interessati da Picture in Picture</li> <li> **Dati **<br/>contestuali (a.media.States.pictureinpicture.set)<br/> </li> <li> **Feed **<br/>di dati media.States.picturereinpicture</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.States.pictureinpicture.set)</li> </ul> |


#### Conteggio immagini

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave **<br/>SDK impostata automaticamente</li> <li> **Chiave **<br/>API N/D</li> <li> **Numero richiesto **<br/></li> <li> **Numero tipo **<br/></li> <li> **Inviato con **<br/>chiusura file multimediali</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Valore **<br/>campione TRUE</li><li> ****<br/>Descrizione: il numero di volte in cui è stato visualizzato Picture in Picture. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato Picture in Picture.<br/> **Importante** <br/> Se questo evento è impostato, il conteggio è uguale al numero di volte in cui il video era nello stato Picture in Picture. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.States.pictureinpicture.count)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponibile **<br/>Sì</li> <li> **Evento variabile **<br/>riservata</li> <li> **Nome **<br/>report Picture in Picture Count</li> <li> **Dati **<br/>contestuali (media.States.pictureinpicture.count)<br/> </li> <li> **Feed **<br/>dati media.States.pictureinpicture.count</li> <li> **Audience Manager **<br/>(c_contextdata.media.States.pictureinpicture.count)</li> </ul> |


#### Durata totale immagine

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave **<br/>SDK impostata automaticamente</li> <li> **Chiave **<br/>API N/D</li> <li> **Numero richiesto **<br/></li> <li> **Numero tipo **<br/></li> <li> **Inviato con **<br/>chiusura file multimediali</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Valore **<br/>campione TRUE</li><li> ****<br/>DescrizioneDurata della visualizzazione Immagine nell&#39;immagine. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato Picture in Picture.<br/> **Importante** <br/> Se questo evento è impostato, l’ora è uguale a quanto tempo il video è stato nello stato Picture in Picture. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.States.pictureinpicture.time)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponibile **<br/>Sì</li> <li> **Evento variabile **<br/>riservata</li> <li> **Nome **<br/>rapporto Immagine nella durata totale</li> <li> **Dati **<br/>contestuali (media.States.pictureinpicture.time)<br/> </li> <li> **Feed **<br/>dati media.States.pictureinpicture.time</li> <li> **Audience Manager **<br/>(c_contextdata.media.States.pictureinpicture.time)</li> </ul> |


### Proprietà dello stato attivo

#### Streams interessati da In Focus

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave **<br/>SDK impostata automaticamente</li> <li> **Chiave **<br/>API N/D</li> <li> **Numero richiesto **<br/></li> <li> **Numero tipo **<br/></li> <li> **Inviato con **<br/>chiusura file multimediali</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Valore **<br/>campione TRUE</li><li> ****<br/>Descrizione: il numero di flussi interessati da In Focus. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato attivo.<br/> **Importante** <br/> Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.States.infocus.set)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponibile **<br/>Sì</li> <li> **Evento variabile **<br/>riservata</li> <li> **Streams dei nomi **<br/>dei report interessati da In Focus</li> <li> **Dati **<br/>contestuali (a.media.States.infocus.set)<br/> </li> <li> **Feed **<br/>dati media.States.infocus</li> <li> **Audience Manager **<br/>(c_contextdata.a.media.States.infocus.set)</li> </ul> |


#### Conteggi per area di interesse

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave **<br/>SDK impostata automaticamente</li> <li> **Chiave **<br/>API N/D</li> <li> **Numero richiesto **<br/></li> <li> **Numero tipo **<br/></li> <li> **Inviato con **<br/>chiusura file multimediali</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Valore **<br/>campione TRUE</li><li> ****<br/>Descrizione: il numero di volte in cui è stato visualizzato In stato attivo. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato attivo.<br/> **Importante **<br/>Se questo evento è impostato, il conteggio è uguale al numero di volte in cui il video si trovava nello stato Attivo. Se questo evento non è impostato, non viene inviato alcun valore.</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.stati.infocus.count)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponibile **<br/>Sì</li> <li> **Evento variabile **<br/>riservata</li> <li> **Nome **<br/>report nel conteggio dello stato attivo</li> <li> **Dati **<br/>contestuali (media.States.infocus.count)<br/> </li> <li> **Feed **<br/>dati media.States.infocus.count</li> <li> **Audience Manager **<br/>(c_contextdata.media.States.infocus.count)</li> </ul> |


#### Durata totale messa a fuoco

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave **<br/>SDK impostata automaticamente</li> <li> **Chiave **<br/>API N/D</li> <li> **Numero richiesto **<br/></li> <li> **Numero tipo **<br/></li> <li> **Inviato con **<br/>chiusura file multimediali</li> <li> **Min. SDK Version **<br/>3.0</li> <li> **Valore **<br/>campione TRUE</li><li> ****<br/>Descrizione: il tempo di attivazione visualizzato. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato attivo.<br/> **Importante** <br/> Se questo evento è impostato, l’ora è uguale a quanto tempo il video è stato nello stato Attivo. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.States.infocus.time)<br/></li> <li> **Heartbeat **<br/>N/D</li> </ul> | <ul> <li> **Disponibile **<br/>Sì</li> <li> **Evento variabile **<br/>riservata</li> <li> **Durata totale del nome **<br/>del report attivo</li> <li> **Dati **<br/>contestuali (media.States.infocus.time)<br/> </li> <li> **Feed **<br/>dati media.States.infocus.time</li> <li> **Audience Manager **<br/>(c_contextdata.media.States.infocus.time)</li> </ul> |



## API correlate {#related_apis_section}

* Android - [createStateObject](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* iOS - [createStateObjectWithName](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* Javascript - [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)