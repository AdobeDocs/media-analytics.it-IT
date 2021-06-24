---
title: Parametri di qualità
description: Scopri i parametri Quality of Experience (QoE) utilizzati per acquisire metadati di qualità.
uuid: 0d9fa764-edef-4178-8650-90c9a0852a57
exl-id: aac178dc-5a46-4ce3-80e9-ec82cbfbfff5
feature: '"Media Analytics, variabili"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '2976'
ht-degree: 2%

---

# Parametri di qualità{#quality-parameters}

Questo argomento presenta un elenco dei dati sulla qualità dell’esperienza (QoE/QoS), inclusi i valori dei dati contestuali, che l’Adobe raccoglie tramite variabili della soluzione.

Descrizione dei dati della tabella:

* **Implementazione:** informazioni su valori e requisiti di implementazione
   * *Chiave* : variabile, impostata manualmente nell’app o automaticamente dall’SDK di Adobe Medium.
   * *Obbligatorio*  - Indica se il parametro è necessario per il tracciamento video di base.
   * *Tipo*  - Specifica il tipo di variabile da impostare, stringa o numero.
   * *Inviato con* : indica quando i dati vengono inviati:  *Media* Startis è la chiamata di analisi inviata all’avvio di un file multimediale,  *Ad* Startis è la chiamata di analisi inviata all’avvio di un annuncio e così via; i  ** Closecalls sono le chiamate di analisi compilate inviate direttamente dal server heartbeat al server analytics alla fine della sessione multimediale, o la fine dell&#39;annuncio, del capitolo, ecc. Le chiamate di chiusura non sono disponibili nelle chiamate dei pacchetti di rete.
   * *Min Versione SDK* - Indica la versione SDK necessaria per accedere al parametro.
   * *Valore di esempio*  - Fornisce un esempio di utilizzo comune delle variabili.
* **Parametri di rete:** visualizza i valori passati ai server Adobe Analytics o Heartbeat. Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate dagli SDK di Adobe Medium.
* **Rapporti:** informazioni su come visualizzare e analizzare i dati video.
   * *Disponibile*  - Indica se i dati sono disponibili nel reporting per impostazione predefinita (*Sì*) o richiede una configurazione personalizzata (*Personalizzato*)
   * *Variabile riservata*  - Indica se i dati vengono acquisiti come evento, eVar, prop o classificazione in una variabile riservata.
   * *Nome report* : nome del report Adobe Analytics per la variabile
   * *Dati contestuali* : nome dei dati contestuali di Adobe Analytics passati al server di reporting e utilizzati nelle regole di elaborazione.
   * *Feed di dati* : nome della colonna per la variabile trovata nei feed di dati Clickstream o Live Stream
   * *Audience Manager* : nome della caratteristica trovato in Adobe Audience Manager

## Metadati qualità {#quality-metadata}

### Bitrate medio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media.qoe.bitrate </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 800-899 </li><li> **Descrizione:**<br/> il bitrate medio (in kbps). Il valore è bucket predefiniti a intervalli di 100 kbps. Il bitrate medio è calcolato come media ponderata di tutti i valori del bitrate relativi alla durata di riproduzione che si è verificata durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>bitrateAverageBucket) </li> <li> **Heartbeat:**<br/>  (:stream:bitrate) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome rapporto: bitrate**<br/> medio </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>bitrateAverageBucket) </li> <li> **Feed di dati:**<br/> videoqoebitrateaverageevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverageBucket) </li> </ul> |


### Ora di inizio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.qoe.timeToStart </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Media Start, Media Close </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 30.000 </li><li> **Descrizione:**<br/> questo valore viene impostato per impostazione predefinita su zero se non lo si imposta tramite l’oggetto QoSO. Questo valore viene impostato in millisecondi. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>timeToStart) </li> <li> **Heartbeat:**<br/>  (:stream:lstartup_time) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome rapporto:**<br/> ora di inizio </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>timeToStart) </li> <li> **Feed di dati:**<br/> videoqoetimetostartevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |


### FPS

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.qoe.framePerSecond </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Media Start, Media Close </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 24 </li><li> **Descrizione:**<br/> il valore corrente del frame rate del flusso (in fotogrammi al secondo).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/>  (:stream:lfps) </li> </ul> | <ul> <li> **Disponibile:**<br/> No </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> N/D </li> <li> **Dati contestuali:**<br/> </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Frame rilasciati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> dropFrames </li> <li> **Chiave API:**<br/> media.qoe.dropFrames </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 3 </li><li> **Descrizione:**<br/> il numero di fotogrammi saltati (Int). Questo valore viene calcolato come somma di tutti i fotogrammi saltati durante una sessione di riproduzione. Questo valore viene ricavato dall&#39;ultimo valore di (l:stream:drop_frame).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>dropFrameCount) </li> <li> **Heartbeat:**<br/>  (:stream:<br/>ldrop_frame) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome rapporto:**<br/> fotogrammi saltati </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>dropFrameCount) </li> <li> **Feed di dati:**<br/> videoqoedroppedframecountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>dropFrameCount) </li> </ul> |



### Eventi buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 2 </li><li> **Descrizione:**<br/> il numero di eventi del buffer. Questa metrica viene calcolata come conteggio dei diversi stati del buffer che si sono verificati durante una sessione di riproduzione. Si tratta di un conteggio del numero di volte in cui il lettore entra in uno stato di buffer da altri stati, ad esempio riproduzione o pausa.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>bufferCount) </li> <li> **Heartbeat:**<br/> (:event:<br/>stype=buffer) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome rapporto:**<br/> Eventi buffer </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>bufferCount) </li> <li> **Feed di dati:**<br/> videoqoebuffercountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### Durata totale buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** </li> <li> **Valore di esempio:**<br/> 30 </li><li> **Descrizione:**<br/> la quantità totale di tempo, in secondi, impiegato nel buffering. Questo valore viene calcolato come somma di tutte le durate degli eventi buffer che si sono verificati durante una sessione di riproduzione. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi. <br/>**Data di rilascio: 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>bufferTime) </li> <li> **Heartbeat:**<br/>  (:event:durata) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome rapporto:**<br/> Durata totale buffer </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>bufferTime) </li> <li> **Feed di dati:**<br/> videoqoebuffertimevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



### Modifiche bitrate

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.qoe.bitrateChange </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 3 </li><li> **Descrizione:**<br/> il numero di modifiche del bitrate (numero intero). Questo valore viene calcolato come somma di tutti gli eventi di cambiamento del bitrate che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>bitrateChangeCount) </li> <li> **Heartbeat:**<br/> (:event:<br/>stype=bitrate_change) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome rapporto:**<br/> modifiche del bitrate </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>bitrateChangeCount) </li> <li> **Feed di dati:**<br/> videoqoebitratechangecountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### Errori / Eventi di errore

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 1 </li><li> **Descrizione:**<br/> il numero di errori (numero intero). Questo valore viene calcolato come somma di tutti gli eventi di errore verificatisi durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>errorCount) </li> <li> **Heartbeat:**<br/>  (:event:<br/>stype=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome rapporto:**<br/> Errori </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>errorCount) </li> <li> **Feed di dati:**<br/> videoqoeerrorcountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



### ID errore SDK del lettore

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> gli ID di errore univoci generati dall’SDK del lettore. I clienti devono fornire i codici/ID di errore al momento dell’implementazione tramite API di errore fornite.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>playerSdkErrors) </li> <li> **Heartbeat:**<br/>  (:event:<br/>stype=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome rapporto:**<br/> ID errore SDK del lettore </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>playerSdkErrors) </li> <li> **Feed di dati:**<br/> videoqoeplayersdkerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>playerSdkErrors) </li> </ul> |



### ID errore esterni

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> gli ID di errore univoci da qualsiasi origine esterna, ad esempio errori CDN. I clienti devono fornire i codici/ID di errore al momento dell’implementazione tramite API di errore fornite.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>externalErrors) </li> <li> **Heartbeat:**<br/>  (:event:<br/>stype=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome rapporto:**<br/> ID errore esterni </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>externalErrors) </li> <li> **Feed di dati:**<br/> videoqoeextneralerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>externalErrors) </li> </ul> |



### ID errore Media SDK

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> gli ID di errore univoci generati dall’SDK Media durante la riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>mediaSdkErrors) </li> <li> **Heartbeat:**<br/>  (:event:<br/>stype=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome rapporto:**<br/> personalizzato </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>mediaSdkErrors) </li> <li> **Feed di dati:**<br/> mediaqoeexternalerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>mediaSdkErrors) </li> </ul><br/> |




### Fine sessione {#session-end}

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** 2.1 </li> <li> **Valore di esempio:**<br/> end </li><li> **Descrizione:**<br/> l’evento finale indica che l’SDK sta inviando una chiamata di chiusura al backend. Al ricevimento dell’evento, il backend chiuderà la sessione per questo video e non eseguirà ulteriori elaborazioni. <br/>Se il contenuto multimediale è stato completato al 100%, questo deve essere inviato dopo  `s:event:type=complete.` Consulta  [Completamento contenuto ](audio-video-parameters.md#content-complete) per le informazioni correlate. </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **heartbeat:**<br/>  (:event:tipo=end) </li> </ul> | <ul> <li> **Disponibile:**<br/> utilizza una regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> N/D </li> <li> **Dati contestuali:**<br/> </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> </li> </ul> |



## Metriche di qualità {#quality-metrics}

### Ora di inizio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 30.000 </li><li> **Descrizione:**<br/> questo valore viene impostato per impostazione predefinita su zero se non lo si imposta tramite l’oggetto QoSO. Questo valore viene impostato in millisecondi. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi. <br/>**Data di rilascio: 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>timeToStart) </li> <li> **Heartbeat:**<br/>  (:stream:lstartup_time) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> ora di inizio </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>timeToStart) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |



### Eventi buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 2 </li><li> **Descrizione:**<br/> il numero di eventi del buffer (Integer). Questa metrica viene calcolata come un conteggio degli eventi buffer che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>bufferCount) </li> <li> **Heartbeat:**<br/> (:event:<br/>stype=buffer) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Eventi buffer </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>bufferCount) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### Durata totale buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 15 </li><li> **Descrizione:**<br/> la quantità totale di tempo impiegato nel buffering (secondi; integer). Questo valore viene calcolato come somma di tutte le durate degli eventi buffer che si sono verificati durante una sessione di riproduzione. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi. <br/>**Data di rilascio: 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>bufferTime) </li> <li> **Heartbeat:**<br/>  (:event:durata) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Durata totale buffer </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>bufferTime) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



### Modifiche bitrate

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> Evento </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> &quot;3&quot; </li><li> **Descrizione:**<br/> il numero di modifiche del bitrate. Questo valore viene calcolato come somma di tutti gli eventi di cambiamento del bitrate che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>bitrateChangeCount) </li> <li> **Heartbeat:**<br/> (:event:<br/>stype=bitrate_change) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> modifiche del bitrate </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>bitrateChangeCount) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### Errori

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 1 </li><li> **Descrizione:**<br/> il numero di errori che si sono verificati (numero intero). Questo valore viene calcolato come somma di tutti gli eventi di errore verificatisi durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>errorCount) </li> <li> **Heartbeat:**<br/>  (:event:<br/>stype=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Eventi di errore </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>errorCount) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



### Frame rilasciati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 1 </li><li> **Descrizione:**<br/> il numero di fotogrammi saltati (numero intero). Questo valore viene calcolato come somma di tutti i fotogrammi saltati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>dropFrameCount) </li> <li> **Heartbeat:**<br/>  (:stream:<br/>ldrop_frame) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> fotogrammi saltati </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>dropFrameCount) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>dropFrameCount) </li> </ul> |



### Rilasci prima dell&#39;inizio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di volte in cui un utente ha abbandonato il video prima del suo avvio. Questa metrica è impostata su 1 solo se non è stato eseguito il rendering di alcun contenuto, indipendentemente dagli annunci.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>dropBeforeStart) </li> <li> **Heartbeat:**<br/> (:event:<br/>stype=aa_start) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> perdite prima dell’avvio </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>dropBeforeStart) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>dropBeforeStart) </li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Flussi interessati dal buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di flussi interessati dal buffering. Questa metrica è impostata su 1 solo se si è verificato almeno un evento buffer durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>tampone) </li> <li> **Heartbeat:**<br/> (:event:<br/>stype=buffer) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> flussi interessati dal buffer </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>tampone) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>tampone) </li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Flussi interessati dalla modifica del bitrate

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di flussi in cui si sono verificate le modifiche del bitrate. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno un evento di cambiamento del bitrate.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>bitrateChange) </li> <li> **Heartbeat:**<br/> (:event:<br/>stype=bitrate_change) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> flussi interessati dalla modifica del bitrate </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>bitrateChange) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChange) </li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Bitrate medio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 3200 </li><li> **Descrizione:**<br/> il bitrate medio (in kbps, numero intero). Questa metrica viene calcolata come media ponderata di tutti i valori di bitrate relativi alla durata di riproduzione che si è verificata durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>bitrateAverage) </li> <li> **Heartbeat:**<br/>  (:stream:bitrate) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto: bitrate**<br/> medio </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>bitrateAverage) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverage) </li> </ul> |



### Flussi interessati dall&#39;errore

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di flussi in cui si è verificato un evento di errore (ovvero,  `trackError` è stato chiamato durante la sessione di riproduzione ed è stata generata una chiamata  `type=error` heartbeat). </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>error) </li> <li> **Heartbeat:**<br/>  (:event:<br/>stype=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> flussi interessati dagli errori </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>error) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>error) </li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Flussi interessati da fotogrammi saltati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di flussi in cui i fotogrammi sono stati eliminati. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione è stato eliminato almeno un fotogramma.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>dropFrames) </li> <li> **Heartbeat:**<br/>  (:stream:<br/>ldrop_frame) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> flussi interessati da fotogrammi saltati </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>dropFrames) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>dropFrames) </li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Stallo dei flussi interessati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** 1.5+ </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di flussi in cui si è verificato un evento in stallo. Questa metrica è impostata su 1 solo se si è verificato almeno un arresto durante la riproduzione. I clienti dovranno creare le proprie regole di elaborazione per disporre del valore disponibile per il reporting.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>stall) </li> <li> **Heartbeat:**<br/> (:event:<br/>stype=stall) </li> </ul> | <ul> <li> **Disponibile:**<br/> utilizza una regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> personalizzato</li> <li> **Feed di dati:**<br/> N/D </li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>stall) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stall) </li> </ul><br/> |

>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Stallo degli eventi

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** 1.5+ </li> <li> **Valore di esempio:**<br/> &quot;3&quot; </li><li> **Descrizione:**<br/> il numero di volte in cui la riproduzione è stata arrestata durante una sessione di riproduzione. I clienti dovranno creare le proprie regole di elaborazione per disporre del valore disponibile per il reporting.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>stallCount) </li> <li> **Heartbeat:**<br/> (:event:<br/>stype=stall) </li> </ul> | <ul> <li> **Disponibile:**<br/> utilizza una regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> personalizzato</li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>stallCount) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stallCount) </li> </ul><br/> |



### Durata totale dello stallo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiusura file multimediali </li> <li> **Min Versione SDK:** 1.5+ </li> <li> **Valore di esempio:**<br/> 12 </li><li> **Descrizione:**<br/> il tempo totale (secondi; integer) la riproduzione è stata arrestata durante una sessione di riproduzione. I clienti dovranno creare le proprie regole di elaborazione per disporre del valore disponibile per il reporting.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.qoe)<br/>stallTime) </li> <li> **Heartbeat:**<br/> (:event:<br/>stype=stall) </li> </ul> | <ul> <li> **Disponibile:**<br/> utilizza una regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> personalizzato</li> <li> **Dati contestuali:**<br/>  (a.media.qoe)<br/>stallTime) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stallTime) </li> </ul> <br/> |



## API correlate {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
