---
seo-title: Parametri di qualità
title: Parametri di qualità
uuid: 0 d 9 fa 764-edef -4178-8650-90 c 9 a 0852 a 57
translation-type: tm+mt
source-git-commit: aca428989370037efcb82ca9af342c904c3d9bce

---


# Quality parameters{#quality-parameters}

Questo argomento presenta un elenco dei dati relativi alla qualità dell'esperienza (qoe/qos), compresi i valori dei dati contestuali, che Adobe raccoglie tramite variabili della soluzione.

Descrizione dati tabella:

* **Implementazione:** Informazioni sui valori e i requisiti di implementazione
   * *Chiave* - Variabile, impostata manualmente nell'app o automaticamente da Adobe Media SDK.
   * *Obbligatorio* - Indica se il parametro è obbligatorio per il tracciamento video di base.
   * *Tipo* : specifica il tipo della variabile da impostare, stringa o numero.
   * *Inviato con* - Indica la data di invio dei dati: *Media Start* è la chiamata di analisi inviata sull'avvio dei supporti, *Ad Avvio* è la chiamata di analisi inviata all'avvio e così via. Le *chiamate Close* sono le chiamate di analisi compilate inviate direttamente dal server heartbeat al server di analisi alla fine della sessione multimediale, o alla fine dell'annuncio, del capitolo, ecc. Le chiamate close non sono disponibili nelle chiamate del pacchetto di rete.
   * *Min. SDK Version* - Indicates which SDK version you would need to access the parameter.
   * *Valore di esempio* - Fornisce esempi di utilizzo variabile delle variabili.
* **Parametri di rete:** Visualizza i valori passati ai server Adobe Analytics o Heartbeat. Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate da Adobe Media SDK.
* **Reporting:** Informazioni su come visualizzare e analizzare i dati video.
   * *Disponibile* - Indica se i dati sono disponibili nel reporting per impostazione predefinita (*Yes*) o richiedono un set personalizzato (*personalizzato*)
   * *Variabile riservata* - Indica se i dati sono acquisiti come evento, evar, prop o classificati in una variabile riservata.
   * *Nome rapporto* - Nome del rapporto Adobe Aanlytics per la variabile
   * *Dati contestuali* - Nome dei dati contestuali di Adobe Analytics passati al server di reporting e utilizzati nelle regole di elaborazione.
   * *Feed dati* - Nome colonna per la variabile trovata nei feed dati Clickstream o Live Stream
   * *Audience Manager* - Nome caratteristica trovato in Adobe Audience Manager

## Quality Metadata {#section_8467F9729DA04A888A2657712234D7C7}

### Bitrate medio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media. qoe. bitrate </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> 800-899 </li><li> **Descrizione:**<br/>Bitrate medio (in kbps). Il valore è intervalli predefiniti a intervalli di 100 kbps. Il bitrate medio viene calcolato come media ponderata di tutti i valori di bitrate relativi alla durata di riproduzione che si è verificata durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitrateaveragebucket) </li> <li> **Heartbeat:**<br/> (l: stream: bitrate) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Bitrate medio </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Bitrateaveragebucket) </li> <li> **Feed dati:**<br/> videoqoebitrateaverageevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitrateaveragebucket) </li> </ul> |



### Tempo di inizio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media. qoe. timetostart </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> 30,000 </li><li> **Descrizione:**<br/>Questo valore predefinito è zero se non viene impostato tramite qosobject. Il valore viene impostato in millisecondi. Il valore verrà visualizzato nel formato temporale (HH: MM: SS) in Analysis Workspace e Reporting e analisi. In Feed dati, Data Warehouse e API di reporting i valori saranno visualizzati in secondi.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Heartbeat:**<br/> (l: stream: startup_ time) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Tempo di inizio </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Feed dati:**<br/> videoqoetimetostartevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>timeToStart) </li> </ul> |



### FPS

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media. qoe. framespersecond </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> 24 </li><li> **Descrizione:**<br/>Il valore corrente della frequenza fotogrammi di streaming (in fotogrammi al secondo).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> (l: stream: fps) </li> </ul> | <ul> <li> **Disponibile:**<br/> No </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> N/D </li> <li> **Dati contestuali:**<br/> </li> <li> **Feed di dati:**<br/> </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Fotogrammi rilasciati

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Droppedframes </li> <li> **Chiave API:**<br/> media. qoe. droppedframes </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> 3 </li><li> **Descrizione:**<br/>Numero di fotogrammi rilasciati (Integer). Questo valore viene calcolato come una somma di tutti i fotogrammi rilasciati durante una sessione di riproduzione. Questo valore è seguito dall'ultimo valore di (l: stream: dropped_ frames.)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Heartbeat:**<br/> (l: stream:<br/>dropped_ frames) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Fotogrammi rilasciati </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Feed dati:**<br/> videoqoedroppedframecountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Droppedframecount) </li> </ul> |



### Eventi buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> 2 </li><li> **Descrizione:**<br/>Numero di eventi buffer. Questa metrica viene calcolata come conteggio dei diversi stati buffer verificatisi durante una sessione di riproduzione. Questo è un totale di quante volte il lettore inserisce uno stato del buffer da altri stati, ad es. riproduzione o pausa.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = buffer </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Eventi buffer </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Feed dati:**<br/> videoqoebuffercountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffercount) </li> </ul> |



### Durata buffer totale

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. Versione SDK:** </li> <li> **Valore campione:**<br/> 30 </li><li> **Descrizione:**<br/>Il tempo totale, in secondi, trascorso il buffering. Questo valore viene calcolato come una somma di tutte le durate di eventi buffer che si sono verificate durante una sessione di riproduzione. Il valore verrà visualizzato nel formato temporale (HH: MM: SS) in Analysis Workspace e Reporting e analisi. In Feed dati, Data Warehouse e API di reporting i valori saranno visualizzati in secondi. <br/>**Data di rilascio: 09/13/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Heartbeat:**<br/> (l: evento: duration) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Durata buffer totale </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Feed dati:**<br/> videoqoebuffertimeevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffertime) </li> </ul> |



### Modifiche bitrate

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media. qoe. bitratechange </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> 3 </li><li> **Descrizione:**<br/>Il numero di modifiche bitrate (Integer). Questo valore viene calcolato come una somma di tutti gli eventi change change che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Modifiche bitrate </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Feed dati:**<br/> videoqoebitratechangecountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitratechangecount) </li> </ul> |



### Errori/Eventi errori

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> 1 </li><li> **Descrizione:**<br/>Il numero di errori si è verificato (Integer). Questo valore viene calcolato come una somma di tutti gli eventi di errore che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Errorcount </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Errori </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Errorcount </li> <li> **Feed dati:**<br/> videoqoeerrorcountevar </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Errorcount </li> </ul> |



### ID errore SDK di Player

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>ID errore univoci generati dall'SDK di lettore. I clienti devono fornire i codici/gli ID di errore al momento dell'implementazione tramite API di errore fornite.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Playersdkerrors) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Errori </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Playersdkerrors) </li> <li> **Feed dati:**<br/> videoqoeplayersdkerrors </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Playersdkerrors) </li> </ul> |



### ID errore esterni

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>ID di errore univoci provenienti da qualsiasi origine esterna, ad esempio, errori CDN. I clienti devono fornire i codici/gli ID di errore al momento dell'implementazione tramite API di errore fornite.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Externalerrors) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Errori </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Externalerrors) </li> <li> **Feed dati:**<br/> videoqoeextneralerrors </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Externalerrors) </li> </ul> |



### ID errore di Media SDK

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>ID di errore univoci generati da Media SDK durante la riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Mediasdkerrors) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Errori </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Mediasdkerrors) </li> <li> **Feed dati:**<br/> mediaqoeexternalerrors </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Mediasdkerrors) </li> </ul> |




### Session End {#session-end}

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** 2.1 </li> <li> **Valore campione:**<br/> end </li><li> **Descrizione:**<br/>L'evento end significa che l'SDK sta inviando una chiamata close al backend. Alla ricezione di questo evento, il backend chiude la sessione per il video e non effettua un'ulteriore elaborazione. <br/>Se il supporto è stato completato a 100%, l'invio deve essere inviato dopo `s:event:type=complete.` il completamento del [contenuto per](audio-video-parameters.md#content-complete) informazioni correlate. </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> (s: evento: type = end) </li> </ul> | <ul> <li> **Disponibile:**<br/> Utilizzare la regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> N/D </li> <li> **Dati contestuali:**<br/> </li> <li> **Feed di dati:**<br/> </li> <li> **Audience Manager:**<br/> </li> </ul> |



## Quality Metrics {#section_8EB0C9CBC09340C8915E1D2707D0A9EE}

### Tempo di inizio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> 30,000 </li><li> **Descrizione:**<br/>Questo valore predefinito è zero se non viene impostato tramite qosobject. Il valore viene impostato in millisecondi. Il valore verrà visualizzato nel formato temporale (HH: MM: SS) in Analysis Workspace e Reporting e analisi. In Feed dati, Data Warehouse e API di reporting i valori saranno visualizzati in secondi. <br/>**Data di rilascio: 09/13/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Heartbeat:**<br/> (l: stream: startup_ time) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Tempo di inizio </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **Feed dati:**<br/> videoqoetimetostart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>timeToStart) </li> </ul> |



### Eventi buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [Startuptime](./quality-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> 2 </li><li> **Descrizione:**<br/>Il numero di eventi buffer (Integer). Questa metrica viene calcolata come un numero di eventi buffer che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = buffer </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Eventi buffer </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Buffercount) </li> <li> **Feed dati:**<br/> videoqoebuffercount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffercount) </li> </ul> |



### Durata buffer totale

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> 15 </li><li> **Descrizione:**<br/>Il periodo totale di buffering impiegato (secondi; integer). Questo valore viene calcolato come una somma di tutte le durate di eventi buffer che si sono verificate durante una sessione di riproduzione. Il valore verrà visualizzato nel formato temporale (HH: MM: SS) in Analysis Workspace e Reporting e analisi. In Feed dati, Data Warehouse e API di reporting i valori saranno visualizzati in secondi. <br/>**Data di rilascio: 09/13/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Heartbeat:**<br/> (l: evento: duration) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Durata buffer totale </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Buffertime) </li> <li> **Feed dati:**<br/> videoqoebuffertime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Buffertime) </li> </ul> |



### Modifiche bitrate

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> Evento </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> " 3 " </li><li> **Descrizione:**<br/>Il numero di modifiche bitrate. Questo valore viene calcolato come una somma di tutti gli eventi change change che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Modifiche bitrate </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Bitratechangecount) </li> <li> **Feed dati:**<br/> videoqoebitratechangecount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitratechangecount) </li> </ul> |



### Errori

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> 1 </li><li> **Descrizione:**<br/>Il numero di errori che si sono verificati (Integer). Questo valore viene calcolato come una somma di tutti gli eventi di errore che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Errorcount </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Eventi errore </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Errorcount </li> <li> **Feed dati:**<br/> videoqoeerrorcount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Errorcount </li> </ul> |



### Fotogrammi rilasciati

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> 1 </li><li> **Descrizione:**<br/>Numero di fotogrammi rilasciati (Integer). Questo valore viene calcolato come una somma di tutti i fotogrammi rilasciati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Heartbeat:**<br/> (l: stream:<br/>dropped_ frames) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Fotogrammi rilasciati </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Droppedframecount) </li> <li> **Feed dati:**<br/> videoqoedroppedframecount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Droppedframecount) </li> </ul> |



### Rilasci prima di iniziare

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> TRUE </li><li> **Descrizione:**<br/>Numero di volte in cui un utente chiude il video prima dell'avvio. Questa metrica è impostata su 1 solo se non è stato eseguito il rendering del contenuto, indipendentemente dagli annunci.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Dropbeforestart) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = aa_ start) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Rilasci prima di iniziare </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Dropbeforestart) </li> <li> **Feed dati:**<br/> videoqoedropbeboschart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Dropbeforestart) </li> </ul> |



>[!IMPORTANT]
>Se l'evento è impostato, l'unico valore possibile è TRUE. Se questo evento non viene impostato, non viene inviato alcun valore.

### Flussi interessati dal buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> TRUE </li><li> **Descrizione:**<br/>Il numero di flussi interessati dal buffering. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno un evento buffer.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>buffer) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = buffer </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Flussi interessati dal buffer </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>buffer) </li> <li> **Feed dati:**<br/> videoqoebuffer </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>Se l'evento è impostato, l'unico valore possibile è TRUE. Se questo evento non viene impostato, non viene inviato alcun valore.

### Flussi interessati Modifica bitrate

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> TRUE </li><li> **Descrizione:**<br/>Il numero di flussi in cui si sono verificati cambiamenti di bitrate. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno un evento di modifica bitrate.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitratechange </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = bitrate_ change) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Flussi interessati dal buffer </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Bitratechange </li> <li> **Feed dati:**<br/> videoqoebitratechange </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitratechange </li> </ul> |



>[!IMPORTANT]
>Se l'evento è impostato, l'unico valore possibile è TRUE. Se questo evento non viene impostato, non viene inviato alcun valore.

### Bitrate medio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> 3200 </li><li> **Descrizione:**<br/>Bitrate medio (in kbps, integer). Questa metrica viene calcolata come media ponderata di tutti i valori di bitrate relativi alla durata di riproduzione che si è verificata durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Bitrateaverage </li> <li> **Heartbeat:**<br/> (l: stream: bitrate) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Bitrate medio </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Bitrateaverage </li> <li> **Feed dati:**<br/> videoqoebitratemedia </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Bitrateaverage </li> </ul> |



### Flussi interessati dall'errore

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> TRUE </li><li> **Descrizione:**<br/>Il numero di flussi in cui si è verificato un evento di errore è `trackError` stato chiamato durante la sessione di riproduzione ed è stata `type=error` generata una chiamata heartbeat. </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>error) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Flussi interessati dall'errore </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>error) </li> <li> **Feed dati:**<br/> videoqoeerror </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>error) </li> </ul> |



>[!IMPORTANT]
>Se l'evento è impostato, l'unico valore possibile è TRUE. Se questo evento non viene impostato, non viene inviato alcun valore.

### Flussi interessati da fotogrammi rilasciati

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> TRUE </li><li> **Descrizione:**<br/>Il numero di flussi in cui sono stati rilasciati i fotogrammi. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione è stato rilasciato almeno un fotogramma.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Droppedframes) </li> <li> **Heartbeat:**<br/> (l: stream:<br/>dropped_ frames) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Flussi interessati da fotogrammi rilasciati </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Droppedframes) </li> <li> **Feed dati:**<br/> videoqoedroppedframes </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Droppedframes) </li> </ul> |



>[!IMPORTANT]
>Se l'evento è impostato, l'unico valore possibile è TRUE. Se questo evento non viene impostato, non viene inviato alcun valore.

### Flussi interessati dall'allineamento

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** 1.5+ </li> <li> **Valore campione:**<br/> TRUE </li><li> **Descrizione:**<br/>Il numero di flussi in cui si è verificato un evento bloccato. Questa metrica è impostata su 1 solo se durante la riproduzione è avvenuta almeno una stall. I clienti dovranno creare le proprie regole di elaborazione per rendere disponibile il valore per il reporting.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>stall) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = stall </li> </ul> | <ul> <li> **Disponibile:**<br/> Utilizzare la regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> </li> <li> **Feed dati:**<br/> N/D </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>stall) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>stall) </li> </ul> |



>[!IMPORTANT]
>Se l'evento è impostato, l'unico valore possibile è TRUE. Se questo evento non viene impostato, non viene inviato alcun valore.

### Staging Events

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** 1.5+ </li> <li> **Valore campione:**<br/> " 3 " </li><li> **Descrizione:**<br/>Il numero di volte in cui la riproduzione è stata bloccata durante una sessione di riproduzione. I clienti dovranno creare le proprie regole di elaborazione per rendere disponibile il valore per il reporting.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Stallcount) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = stall </li> </ul> | <ul> <li> **Disponibile:**<br/> Utilizzare la regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Stallcount) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Stallcount) </li> </ul> |



### Durata totale della sovrapposizione

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** 1.5+ </li> <li> **Valore campione:**<br/> 12 </li><li> **Descrizione:**<br/>Il tempo totale (secondi; integer) La riproduzione è stata bloccata durante una sessione di riproduzione. I clienti dovranno creare le proprie regole di elaborazione per rendere disponibile il valore per il reporting.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. qoe.<br/>Stalltime) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = stall </li> </ul> | <ul> <li> **Disponibile:**<br/> Utilizzare la regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/> (a. media. qoe.<br/>Stalltime) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. qoe.<br/>Stalltime) </li> </ul> |



## Related APIs {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

