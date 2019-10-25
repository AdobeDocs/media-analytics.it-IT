---
seo-title: Parametri di qualità
title: Parametri di qualità
uuid: 0d9fa764-edef-4178-8650-90c9a0852a57
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# Parametri di qualità{#quality-parameters}

Questo argomento presenta un elenco di dati sulla qualità dell'esperienza (QoE/QoS), inclusi i valori dei dati contestuali, raccolti da Adobe tramite variabili della soluzione.

Descrizione dati tabella:

* **** Implementazione: Informazioni su valori e requisiti di implementazione
   * *Chiave* - Variabile, impostata manualmente nell’app o automaticamente dall’SDK di Adobe Media.
   * *Obbligatorio* - Indica se il parametro è richiesto per il tracciamento video di base.
   * *Tipo* - Specifica il tipo di variabile da impostare, stringa o numero.
   * *Inviato con* - Indica quando i dati vengono inviati: *Media Start* è la chiamata di analisi inviata all’avvio del supporto, *Ad Start* è la chiamata di analisi inviata all’inizio e all’inizio dell’annuncio, e così via; le chiamate *Close* sono le chiamate di analisi compilate inviate direttamente dal server Heartbeat al server di analisi alla fine della sessione multimediale, o la fine dell'annuncio, del capitolo, ecc. Le chiamate di chiusura non sono disponibili nelle chiamate dei pacchetti di rete.
   * *Min. Versione* SDK - Indica la versione SDK a cui sarà necessario accedere per il parametro.
   * *Valore* di esempio - Fornisce un esempio di utilizzo comune delle variabili.
* **** Parametri di rete: Visualizza i valori passati ai server Adobe Analytics o Heartbeat. Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate dagli SDK di Adobe Media.
* **** Reporting: Informazioni su come visualizzare e analizzare i dati video.
   * *Disponibile* - Indica se i dati sono disponibili nel reporting per impostazione predefinita (*Sì*) o richiedono una configurazione personalizzata (*Personalizzato*)
   * *Variabile* riservata - Indica se i dati vengono acquisiti come evento, eVar, prop o classificazione in una variabile riservata.
   * *Nome* report - Nome del report Adobe Analytics per la variabile
   * *Dati* contestuali - Nome dei dati contestuali di Adobe Analytics passati al server di reporting e utilizzati nelle regole di elaborazione.
   * *Feed* dati - Nome colonna per la variabile trovata nei feed di dati Clickstream o Live Stream
   * *Audience Manager* - Nome caratteristica trovato in Adobe Audience Manager

## Metadati qualità {#quality-metadata}

### Bitrate medio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> ****<br/>  Chiave API: media.qoe.bitrate </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiudi </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: 800-899 </li><li> **Descrizione:**<br/>bitrate medio (in kbps). Il valore è bucket predefiniti a intervalli di 100 kbps. Il bitrate medio è calcolato come media ponderata di tutti i valori del bitrate relativi alla durata di riproduzione che si è verificata durante una sessione di riproduzione.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bitrateAverageBucket) </li> <li> ****<br/> Heartbeat: (l:stream:bitrate) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Bitrate medio </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>bitrateAverageBucket) </li> <li> ****<br/> Feed dati: videoqoebitrateaverageevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverageBucket) </li> </ul> |



### Ora di inizio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> ****<br/>  Chiave API: media.qoe.timeToStart </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: 30.000 </li><li> **Descrizione:**<br/>questo valore predefinito è zero se non viene impostato tramite l'oggetto QoSObject. Questo valore viene impostato in millisecondi. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>timeToStart) </li> <li> ****<br/> Heartbeat: (l:stream:start_time) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Ora di inizio </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>timeToStart) </li> <li> ****<br/> Feed dati: videoqetimetostartevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |



### FPS

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> ****<br/>  Chiave API: media.qoe.framePerSecond </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: 24 </li><li> **Descrizione:**<br/>Il valore corrente del frame rate del flusso (in fotogrammi al secondo).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> ****<br/> Heartbeat: (l:stream:fps) </li> </ul> | <ul> <li> ****<br/> Disponibile:No </li> <li> ****<br/> Variabile riservata:N/D </li> <li> ****<br/> Nome rapporto:N/D </li> <li> **Dati contestuali:**<br/> </li> <li> ****<br/> Feed dati:N/D </li> <li> **Audience Manager:**<br/> </li> </ul> |



###  Fotogrammi rilasciati

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: dropFrames </li> <li> ****<br/>  Chiave API: media.qoe.dropFrames </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: 3 </li><li> **Descrizione:**<br/>il numero di fotogrammi saltati (Int). Questo valore viene calcolato come somma di tutti i fotogrammi saltati durante una sessione di riproduzione. Questo valore viene ricavato dall’ultimo valore di (l:stream:drop_frame).  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>dropFrameCount) </li> <li> ****<br/> Heartbeat: (l:stream:<br/>drop_frame) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto: Fotogrammi rilasciati </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>dropFrameCount) </li> <li> ****<br/> Feed dati: videoqoedroppedframecountevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>dropFrameCount) </li> </ul> |



### Eventi buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: 2 </li><li> **Descrizione:**<br/>il numero di eventi del buffer. Questa metrica viene calcolata come un conteggio dei diversi stati del buffer che si sono verificati durante una sessione di riproduzione. Si tratta del numero di volte in cui il lettore entra in uno stato di buffer da altri stati, ad esempio la riproduzione o la pausa.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bufferCount) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Eventi buffer </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>bufferCount) </li> <li> ****<br/> Feed dati: videoqoebuffercountevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### Durata totale buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min. Versione SDK:** </li> <li> ****<br/> Valore campione: 30 </li><li> **Descrizione:**<br/>il tempo totale, in secondi, impiegato nel buffer. Questo valore viene calcolato come somma di tutte le durate degli eventi buffer che si sono verificati durante una sessione di riproduzione. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi. <br/>**Data di rilascio: 13/09/18**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bufferTime) </li> <li> ****<br/> Heartbeat: (l:evento:durata) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Durata totale buffer </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>bufferTime) </li> <li> ****<br/> Feed dati: videoqoebuffertimevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



###  Modifiche bitrate

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> ****<br/>  Chiave API: media.qoe.bitrateChange </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: 3 </li><li> **Descrizione:**<br/>il numero di modifiche del bitrate (Integer). Questo valore viene calcolato come somma di tutti gli eventi di modifica del bitrate verificatisi durante una sessione di riproduzione.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bitrateChangeCount) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto: Modifiche bitrate </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>bitrateChangeCount) </li> <li> ****<br/> Feed dati: videoqoebitratechangecountevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### Errori/Eventi di errore

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: 1 </li><li> **Descrizione:**<br/>Numero di errori (Integer). Questo valore viene calcolato come somma di tutti gli eventi di errore che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>errorCount) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=error) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Errori </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>errorCount) </li> <li> ****<br/> Feed dati: videoqoeerrorcountevar </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



### ID errore SDK lettore

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> **Chiave API:**<br/> </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>gli ID di errore univoci generati dall’SDK del lettore. I clienti devono fornire i codici/ID di errore al momento dell'implementazione tramite le API di errore fornite.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>playerSdkErrors) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=error) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Errori </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>playerSdkErrors) </li> <li> ****<br/> Feed dati: videoqoeplayersderrori </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>playerSdkErrors) </li> </ul> |



### ID errore esterni

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> **Chiave API:**<br/> </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>gli ID di errore univoci da qualsiasi origine esterna, ad esempio, errori CDN. I clienti devono fornire i codici/ID di errore al momento dell'implementazione tramite le API di errore fornite.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>externalErrors) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=error) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Errori </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>externalErrors) </li> <li> ****<br/> Feed dati: videoqoeextneralerrori </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>externalErrors) </li> </ul> |



### ID errore Media SDK

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> **Chiave API:**<br/> </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>gli ID di errore univoci generati da Media SDK durante la riproduzione.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>mediaSdkErrors) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=error) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Errori </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>mediaSdkErrors) </li> <li> ****<br/> Feed dati: mediaqoeesternalerrori </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>mediaSdkErrors) </li> </ul> |




### Fine sessione {#session-end}

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> **Chiave API:**<br/> </li> <li> ****<br/> Tipo:string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: 2.1 </li> <li> ****<br/> Valore campione: end </li><li> **Descrizione:**<br/>L’evento end indica che l’SDK sta inviando una chiamata di chiusura al backend. Alla ricezione di questo evento, il backend chiuderà la sessione per il video e non eseguirà ulteriori elaborazioni. <br/>Se il supporto è stato completato al 100%, questo verrà inviato dopo `s:event:type=complete.` Consulta [Contenuto completo](audio-video-parameters.md#content-complete) per le informazioni correlate. </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:N/D </li> <li> ****<br/> Heartbeat: (s:event:type=end) </li> </ul> | <ul> <li> ****<br/> Disponibile: Usa regola di elaborazione personalizzata </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto:N/D </li> <li> **Dati contestuali:**<br/> </li> <li> ****<br/> Feed dati:N/D </li> <li> **Audience Manager:**<br/> </li> </ul> |



## Metriche di qualità {#quality-metrics}

### Ora di inizio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: 30.000 </li><li> **Descrizione:**<br/>questo valore predefinito è zero se non viene impostato tramite l'oggetto QoSObject. Questo valore viene impostato in millisecondi. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi. <br/>**Data di rilascio: 13/09/18**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>timeToStart) </li> <li> ****<br/> Heartbeat: (l:stream:start_time) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto:Ora di inizio </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>timeToStart) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |



### Eventi buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [startTime](./quality-parameters.md#related_apis_section) </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: 2 </li><li> **Descrizione:**<br/>il numero di eventi del buffer (Integer). Questa metrica viene calcolata come conteggio degli eventi del buffer che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bufferCount) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto:Eventi buffer </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>bufferCount) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### Durata totale buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: 15 </li><li> **Descrizione:**<br/>l'importo totale del tempo impiegato (secondi; integer). Questo valore viene calcolato come somma di tutte le durate degli eventi buffer che si sono verificati durante una sessione di riproduzione. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi. <br/>**Data di rilascio: 13/09/18**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bufferTime) </li> <li> ****<br/> Heartbeat: (l:evento:durata) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto:Durata totale buffer </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>bufferTime) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



###  Modifiche bitrate

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: Evento </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: "3" </li><li> **Descrizione:**<br/>il numero di modifiche del bitrate. Questo valore viene calcolato come somma di tutti gli eventi di modifica del bitrate verificatisi durante una sessione di riproduzione.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bitrateChangeCount) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto: Modifiche bitrate </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>bitrateChangeCount) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### Errori

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: 1 </li><li> **Descrizione:**<br/>il numero di errori che si sono verificati (Integer). Questo valore viene calcolato come somma di tutti gli eventi di errore che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>errorCount) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=error) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto: Eventi errore </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>errorCount) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



###  Fotogrammi rilasciati

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: 1 </li><li> **Descrizione:**<br/>il numero di fotogrammi saltati (Integer). Questo valore viene calcolato come somma di tutti i fotogrammi saltati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>dropFrameCount) </li> <li> ****<br/> Heartbeat: (l:stream:<br/>drop_frame) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto: Fotogrammi rilasciati </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>dropFrameCount) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>dropFrameCount) </li> </ul> |



### Rilasci prima dell'avvio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo:string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: TRUE </li><li> **Descrizione:**<br/>il numero di volte in cui un utente ha abbandonato il video prima del suo avvio. Questa metrica è impostata su 1 solo se non è stato eseguito il rendering di alcun contenuto, indipendentemente dagli annunci.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>dropBeforeStart) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=aa_start) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto: Gocce prima dell'inizio </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>dropBeforeStart) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>dropBeforeStart) </li> </ul> |



>[!IMPORTANT]
>Se questo evento è impostato, l'unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

###  Flussi interessati dal buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo:string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: TRUE </li><li> **Descrizione:**<br/>il numero di flussi interessati dal buffering. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno un evento del buffer.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>buffer) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto: Flussi interessati dal buffer </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>buffer) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>Se questo evento è impostato, l'unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

###  Flussi interessati dalle modifiche bitrate

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo:string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: TRUE </li><li> **Descrizione:**<br/>il numero di flussi in cui si sono verificate modifiche al bitrate. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno un evento di modifica del bitrate.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bitrateChange) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto: Flussi interessati dalle modifiche bitrate </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>bitrateChange) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bitrateChange) </li> </ul> |



>[!IMPORTANT]
>Se questo evento è impostato, l'unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Bitrate medio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: 3200 </li><li> **Descrizione:**<br/>bitrate medio (in kbps, numero intero). Questa metrica viene calcolata come media ponderata di tutti i valori del bitrate relativi alla durata di riproduzione che si è verificata durante una sessione di riproduzione.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>bitrateAverage) </li> <li> ****<br/> Heartbeat: (l:stream:bitrate) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto:Bitrate medio </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>bitrateAverage) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverage) </li> </ul> |



### Flussi interessati dall'errore

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo:string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: TRUE </li><li> **Descrizione:**<br/>Il numero di flussi in cui si è verificato un evento di errore (ovvero, `trackError` è stato chiamato durante la sessione di riproduzione ed è stata generata una chiamata `type=error` heartbeat). </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>error) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=error) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto:Flussi interessati dall'errore </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>error) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>error) </li> </ul> |



>[!IMPORTANT]
>Se questo evento è impostato, l'unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

###  Flussi interessati da fotogrammi rilasciati

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo:string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: TRUE </li><li> **Descrizione:**<br/>il numero di flussi in cui i fotogrammi sono stati eliminati. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione è stato eliminato almeno un fotogramma.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>dropFrames) </li> <li> ****<br/> Heartbeat: (l:stream:<br/>drop_frame) </li> </ul> | <ul> <li> ****<br/> Disponibile:Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto: Flussi interessati da fotogrammi rilasciati </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>dropFrames) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>dropFrames) </li> </ul> |



>[!IMPORTANT]
>Se questo evento è impostato, l'unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Stallo dei flussi interessati

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo:string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: 1,5+ </li> <li> ****<br/> Valore campione: TRUE </li><li> **Descrizione:**<br/>il numero di flussi in cui si è verificato un evento in stallo. Questa metrica è impostata su 1 solo se durante la riproduzione si è verificato almeno un arresto. I clienti dovranno creare le proprie regole di elaborazione per avere il valore disponibile per il reporting.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>stall) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=stall) </li> </ul> | <ul> <li> ****<br/> Disponibile: Usa regola di elaborazione personalizzata </li> <li> ****<br/> Variabile riservata:event </li> <li> **Nome rapporto:**<br/> </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>stall) </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>stall) </li> </ul> |



>[!IMPORTANT]
>Se questo evento è impostato, l'unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Stallo degli eventi

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo:string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: 1,5+ </li> <li> ****<br/> Valore campione: "3" </li><li> **Descrizione:**<br/>il numero di volte in cui la riproduzione è stata bloccata durante una sessione di riproduzione. I clienti dovranno creare le proprie regole di elaborazione per avere il valore disponibile per il reporting.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>stallCount) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=stall) </li> </ul> | <ul> <li> ****<br/> Disponibile: Usa regola di elaborazione personalizzata </li> <li> ****<br/> Variabile riservata:event </li> <li> **Nome rapporto:**<br/> </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>stallCount) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>stallCount) </li> </ul> |



### Durata totale arresto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/>  Chiave API:N/D </li> <li> ****<br/> Obbligatorio:No </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: 1,5+ </li> <li> ****<br/> Valore campione: 12 </li><li> **Descrizione:**<br/>Tempo totale (secondi; integer) la riproduzione è stata bloccata durante una sessione di riproduzione. I clienti dovranno creare le proprie regole di elaborazione per avere il valore disponibile per il reporting.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.qoe.<br/>stallTime) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=stall) </li> </ul> | <ul> <li> ****<br/> Disponibile: Usa regola di elaborazione personalizzata </li> <li> ****<br/> Variabile riservata:event </li> <li> **Nome rapporto:**<br/> </li> <li> ****<br/> Dati contestuali: (a.media.qoe.<br/>stallTime) </li> <li> ****<br/> Feed dati:N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.qoe.<br/>stallTime) </li> </ul> |



## API correlate {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

