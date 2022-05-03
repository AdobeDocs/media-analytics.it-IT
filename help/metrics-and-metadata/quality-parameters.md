---
title: 'Parametri per la qualità '
description: Scopri i parametri Quality of Experience (QoE) utilizzati per acquisire metadati di qualità.
uuid: 0d9fa764-edef-4178-8650-90c9a0852a57
exl-id: aac178dc-5a46-4ce3-80e9-ec82cbfbfff5
feature: Media Analytics, Variables
role: User, Admin, Data Engineer
source-git-commit: 6e01f55ac498d69a6f7eac4ac0086e276cc0dd8a
workflow-type: ht
source-wordcount: '3106'
ht-degree: 100%

---

# Parametri per la qualità {#quality-parameters}

Questo argomento presenta un elenco dei dati sulla qualità dell’esperienza (QoE/QoS), inclusi i valori dei dati contestuali, che Adobe raccoglie tramite variabili della soluzione.

Descrizione dei dati della tabella:

* **Implementazione:** informazioni su valori e requisiti di implementazione
   * *Chiave* - Variabile, impostata manualmente nell’app o automaticamente dall’SDK di Adobe Media.
   * *Obbligatorio* - Indica se il parametro è necessario per il tracciamento video di base.
   * *Tipo* - Specifica il tipo di variabile da impostare, stringa o numero.
   * *Inviato con* - Indica quando i dati vengono inviati: *Media Start* è la chiamata di analytics inviata all’avvio del supporto; *Inizio annuncio* è la chiamata di analytics inviata all’inizio dell’annuncio e così via; le chiamate *di chiusura* sono le chiamate analytics compilate inviate direttamente dal server heartbeat al server analytics alla fine della sessione multimediale, o la fine dell’annuncio, del capitolo, ecc. Le chiamate di chiusura non sono disponibili nelle chiamate dei pacchetti di rete.
   * *Versione SDK min.* - Indica la versione SDK necessaria per accedere al parametro.
   * *Valore di esempio* - Fornisce un esempio di utilizzo comune delle variabili.
* **Parametri di rete:** visualizza i valori passati ai server Adobe Analytics o Heartbeat. Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate dagli SDK di Adobe Media.
* **Reporting:** informazioni su come visualizzare e analizzare i dati video.
   * *Disponibile* - Indica se i dati sono disponibili nel reporting per impostazione predefinita (*Sì*) o richiede la configurazione personalizzata (*Personalizzato*)
   * *Variabile riservata* - Indica se i dati vengono acquisiti come evento, eVar, prop o classificazione in una variabile riservata.
   * *Nome del rapporto* - Nome del report Adobe Analytics per la variabile
   * *Dati contestuali* - Nome dei dati contestuali di Adobe Analytics passati al server di reporting e utilizzati nelle regole di elaborazione.
   * *Feed di dati* - Nome della colonna per la variabile trovata nei feed di dati Clickstream o Live Stream
   * *Audience Manager* - Nome delle caratteristiche trovato in Adobe Audience Manager

## Metadati qualità {#quality-metadata}

### Bitrate medio

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media.qoe.bitrate </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiudi </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> 800-899 </li><li> **Descrizione:**<br/> Il bitrate medio (in kbps). Il valore è bucket predefiniti a intervalli di 100 kbps. Il bitrate medio è calcolato come media ponderata di tutti i valori del bitrate relativi alla durata di riproduzione che si è verificata durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **Heartbeat:**<br/> (l:stream:bitrate) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome report:**<br/> bitrate medio </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **Feed dati:**<br/> videoqoebitrateaverageevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverageBucket </li> </ul> |


### Ora di inizio

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.qoe.timeToStart </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Avvio file multimediale, Chiusura file multimediale </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> 30.000 </li><li> **Descrizione:**<br/> se non viene impostato tramite l’oggetto QoSO, il valore predefinito è zero. Questo valore viene impostato in millisecondi. Il valore viene visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **Heartbeat:**<br/> (l:stream:startup_time) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome report:**<br/> ora di inizio </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **Feed dati:**<br/> videoqetimetostartevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart.value </li> </ul> |


### Frame al secondo

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.qoe.framesPerSecond </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Avvio file multimediale, Chiusura file multimediale </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> 24 </li><li> **Descrizione:**<br/> valore corrente del frame rate del flusso (in fotogrammi al secondo). Il campo è mappato al campo fps nella chiamata di chiusura e accessibile tramite regole di elaborazione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> (l:stream:fps) </li> </ul> | <ul> <li> **Disponibile:**<br/> no </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome report:**<br/> N/D </li> <li> **Dati contestuali:**<br/> </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> </li> <li> **Percorso campo XDM:**<br/>  </li> </ul> |



### Frame rilasciati

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> droppedFrames </li> <li> **Chiave API:**<br/> media.qoe.droppedFrames </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> 3 </li><li> **Descrizione:**<br/> numero di fotogrammi saltati (Int). Questo valore viene calcolato come somma di tutti i fotogrammi saltati durante una sessione di riproduzione. Questo valore viene preso dall’ultimo valore di (l:stream:dropped_frames).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Heartbeat:**<br/> (l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome report:**<br/> Frame rilasciati </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Feed dati:**<br/> videoqoedroppedframecountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>droppedFrameCount) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames.value </li> </ul> |



### Eventi buffer

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> 2 </li><li> **Descrizione:**<br/> numero di eventi del buffer. Questa metrica viene calcolata come conteggio dei diversi stati del buffer che si sono verificati durante una sessione di riproduzione. Si tratta di un conteggio del numero di volte in cui il lettore entra in uno stato di buffer da altri stati, ad esempio riproduzione o pausa.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome report:**<br/> eventi buffer </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **Feed dati:**<br/> videoqoebuffercountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.buffers.value </li> </ul> |



### Durata totale buffer

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** </li> <li> **Valore di esempio:**<br/> 30 </li><li> **Descrizione:**<br/> quantità totale di tempo, in secondi, trascorso il buffering. Questo valore viene calcolato come somma di tutte le durate degli eventi buffer che si sono verificati durante una sessione di riproduzione. Il valore viene visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi. <br/>**Data di rilascio: 13/09/18**  **</li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **Heartbeat:**<br/> (l:event:durata) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome report:**<br/> durata totale buffer </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **Feed dati:**<br/> videoqoebuffertimeevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime.value </li> </ul> |



### Modifiche bitrate

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.qoe.bitrateChange </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> 3 </li><li> **Descrizione:**<br/> il numero di modifiche del bitrate (numero intero). Questo valore viene calcolato come somma di tutti gli eventi di cambiamento del bitrate che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome report:**<br/> modifiche bitrate </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Feed dati:**<br/> videoqoebitratechangecountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges.value </li> </ul> |



### Errori / Eventi di errore

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> 1 </li><li> **Descrizione:**<br/> numero di errori (numero intero). Questo valore viene calcolato come somma di tutti gli eventi di errore verificatisi durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome report:**<br/> errori </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **Feed dati:**<br/> videoqoeerrorcountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.errors.value </li> </ul> |



### ID errore SDK del lettore

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> ID di errore univoci generati dall’SDK del lettore. I clienti devono fornire i codici/ID di errore al momento dell’implementazione tramite API di errore fornite.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>playerSdkErrors) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome report:**<br/> ID errore SDK del lettore </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>playerSdkErrors) </li> <li> **Feed dati:**<br/> videoqoeplayersdkerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>playerSdkErrors) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.playerSdkErrors </li> </ul> |



### ID errore esterni

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> ID di errore univoci da qualsiasi origine esterna, ad esempio errori CDN. I clienti devono fornire i codici/ID di errore al momento dell’implementazione tramite API di errore fornite.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>externalErrors) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome report:**<br/> ID errore esterni </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>externalErrors) </li> <li> **Feed dati:**<br/> videoqoeextneralerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>externalErrors) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.externalSdkErrors </li> </ul> |



### ID errore SDK per contenuti multimediali

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> ID di errore univoci generati da SDK per contenuti multimediali durante la riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>mediaSdkErrors) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome report:**<br/> personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>mediaSdkErrors) </li> <li> **Feed dati:**<br/> mediaqoeexternalerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>mediaSdkErrors) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.mediaSdkErrors </li> </ul><br/> |




### Fine sessione {#session-end}

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** 2.1 </li> <li> **Valore di esempio:**<br/> fine </li><li> **Descrizione:**<br/> l’evento finale indica che l’SDK sta inviando una chiamata di chiusura al backend. Al ricevimento dell’evento, il backend chiuderà la sessione per questo video e non eseguirà ulteriori elaborazioni. <br/>Se il supporto è stato completato al 100%, è necessario inviarlo dopo `s:event:type=complete.`. Vedi [Contenuto completato](audio-video-parameters.md#content-complete) per informazioni correlate. </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> (s:event:type=end) </li> </ul> | <ul> <li> **Disponibile:**<br/> usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> N/D </li> <li> **Dati contestuali:**<br/> </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> </li> <li> **Percorso campo XDM:**<br/>  </li> </ul> |



## Metriche di qualità {#quality-metrics}

### Ora di inizio

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> 30.000 </li><li> **Descrizione:**<br/> se non viene impostato tramite l’oggetto QoSO, il valore predefinito è zero. Questo valore viene impostato in millisecondi. Il valore viene visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi. <br/>**Data di rilascio: 13/09/18**  **</li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **Heartbeat:**<br/> (l:stream:startup_time) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> ora di inizio </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart.value </li> </ul> |



### Eventi buffer

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> 2 </li><li> **Descrizione:**<br/> numero di eventi del buffer (numero intero). Questa metrica viene calcolata come un conteggio degli eventi buffer che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> eventi buffer </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.buffers.value </li> </ul> |



### Durata totale buffer

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> 15 </li><li> **Descrizione:**<br/> l’importo totale del tempo impiegato per il buffering (secondi; numero intero). Questo valore viene calcolato come somma di tutte le durate degli eventi buffer che si sono verificati durante una sessione di riproduzione. Il valore viene visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi. <br/>**Data di rilascio: 13/09/18**  **</li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **Heartbeat:**<br/> (l:event:durata) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> durata totale buffer </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime.value </li> </ul> |



### Modifiche bitrate

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> Evento </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> “3” </li><li> **Descrizione:**<br/> il numero di modifiche del bitrate. Questo valore viene calcolato come somma di tutti gli eventi di cambiamento del bitrate che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> modifiche bitrate </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges.value </li> </ul> |



### Errori

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> 1 </li><li> **Descrizione:**<br/> il numero di errori che si sono verificati (numero intero). Questo valore viene calcolato come somma di tutti gli eventi di errore verificatisi durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> Eventi di errore </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.errors.value </li> </ul> |



### Frame rilasciati

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> 1 </li><li> **Descrizione:**<br/> numero di fotogrammi saltati (numero intero). Questo valore viene calcolato come somma di tutti i fotogrammi saltati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Heartbeat:**<br/> (l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> frame rilasciati </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>droppedFrameCount) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>droppedFrameCount) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames.value </li> </ul> |



### Rilasci prima dell’inizio

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di volte in cui un utente ha abbandonato il video prima del suo avvio. Questa metrica è impostata su 1 solo se non è stato eseguito il rendering di alcun contenuto, indipendentemente dagli annunci.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>dropBeforeStart) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=aa_start) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> cadute prima dell’inizio </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>dropBeforeStart) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>dropBeforeStart) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.dropBeforeStarts.value >= 1 => “TRUE” </li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l’unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Flussi interessati dal buffer

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di flussi interessati dal buffering. Questa metrica è impostata su 1 solo se si è verificato almeno un evento buffer durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>buffer) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> flussi interessati dal buffer </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>buffer) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>buffer) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bufferImpactedStreams.value >= 1 => “TRUE” </li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l’unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Flussi interessati dalla modifica del bitrate

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di flussi in cui si sono verificate le modifiche del bitrate. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno un evento di cambiamento del bitrate.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateChange) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> flussi interessati dalla modifica del bitrate </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bitrateChange) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChange) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChangeImpactedStreams.value >= 1 => “TRUE” </li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l’unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Bitrate medio

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> 3200 </li><li> **Descrizione:**<br/> il bitrate medio (in kbps, numero intero). Questa metrica viene calcolata come media ponderata di tutti i valori di bitrate relativi alla durata di riproduzione che si è verificata durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateAverage) </li> <li> **Heartbeat:**<br/> (l:stream:bitrate) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> bitrate medio </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bitrateAverage) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverage) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage.value </li> </ul> |



### Flussi interessati dall’errore

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di flussi in cui si è verificato un evento di errore (ovvero `trackError` è stato chiamato durante la sessione di riproduzione e una chiamata heartbeat `type=error` generata). </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>error) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> Flussi interessati dall’errore </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>error) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>error) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.errorImpactedStreams.value > 0 => “TRUE” </li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l’unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Flussi interessati da fotogrammi saltati

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> numero di flussi in cui i fotogrammi sono stati eliminati. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione è stato eliminato almeno un fotogramma.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>droppedFrames) </li> <li> **Heartbeat:**<br/> (l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> flussi interessati da fotogrammi saltati </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>droppedFrames) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>droppedFrames) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrameImpactedStreams.value >= 1 => “TRUE” </li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l’unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Stallo dei flussi interessati

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** 1.5+ </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di flussi in cui si è verificato un evento in stallo. Questa metrica è impostata su 1 solo se si è verificato almeno un arresto durante la riproduzione. I clienti dovranno creare le proprie regole di elaborazione per disporre del valore disponibile per il reporting.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>stall) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Disponibile:**<br/> usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> personalizzato</li> <li> **Feed dati:**<br/> N/D </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>stall) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stall) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.stallingImpactedStreams.value >= 1 => “TRUE” </li> </ul><br/> |

>[!IMPORTANT]
>
>Se questo evento è impostato, l’unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Stallo degli eventi

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** 1.5+ </li> <li> **Valore di esempio:**<br/> “3” </li><li> **Descrizione:**<br/> numero di volte in cui la riproduzione è stata arrestata durante una sessione di riproduzione. I clienti dovranno creare le proprie regole di elaborazione per disporre del valore disponibile per il reporting.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>stallCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Disponibile:**<br/> usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> personalizzato</li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>stallCount) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stallCount) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.stalls.value </li> </ul><br/> |



### Durata totale dello stallo

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> chiudi file multimediali </li> <li> **Versione SDK min.:** 1.5+ </li> <li> **Valore di esempio:**<br/> 12 </li><li> **Descrizione:**<br/> il tempo totale (secondi; numero intero) in cui la riproduzione è stata arrestata durante una sessione di riproduzione. I clienti dovranno creare le proprie regole di elaborazione per disporre del valore disponibile per il reporting.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>stallTime) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Disponibile:**<br/> usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome report:**<br/> personalizzato</li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>stallTime) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stallTime) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.qoe.stallTime.value </li> </ul> <br/> |



## API correlate {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
