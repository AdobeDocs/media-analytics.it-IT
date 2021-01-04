---
title: Parametri di qualità
description: null
uuid: 0d9fa764-edef-4178-8650-90c9a0852a57
translation-type: tm+mt
source-git-commit: 5802a474588a6df6c66e0d1d7cb2fd30f83e4e3d
workflow-type: tm+mt
source-wordcount: '2992'
ht-degree: 2%

---


# Parametri di qualità{#quality-parameters}

Questo argomento presenta un elenco di dati sulla qualità dell&#39;esperienza (QoE/QoS), inclusi i valori dei dati contestuali, che  Adobe raccoglie tramite variabili della soluzione.

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

## Metadati di qualità {#quality-metadata}

### Bitrate medio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media.qoe.bitrate </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/> 800-899 </li><li> **Descrizione:**<br/> bitrate medio (in kbps). Il valore è bucket predefiniti a intervalli di 100 kbps. Il bitrate medio è calcolato come media ponderata di tutti i valori del bitrate relativi alla durata di riproduzione che si è verificata durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **Heartbeat:**<br/> (l:stream:bitrate) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile Riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> sull&#39;HIT </li> <li> **Nome Report:Bitrate**<br/> Medio </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **Feed dati:**<br/> videoqoebitrateaverageevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverageBucket) </li> </ul> |


### Ora di inizio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.qoe.timeToStart </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:Avvio**<br/> file multimediali, Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 30.000 </li><li> **Descrizione:**<br/> questo valore predefinito è zero se non viene impostato tramite l&#39;oggetto QoSObject. Questo valore viene impostato in millisecondi. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in  Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **Heartbeat:**<br/> (l:stream:start_time) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile Riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> sull&#39;HIT </li> <li> **Nome rapporto:**<br/> Ora di inizio </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **Feed dati:**<br/> videoqoetimetostartevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |


### FPS

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.qoe.framePerSecond </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:Avvio**<br/> file multimediali, Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore Di Esempio:**<br/> 24 </li><li> **Descrizione:**<br/> Il valore corrente del frame rate del flusso (in fotogrammi al secondo).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> (l:stream:fps) </li> </ul> | <ul> <li> **Disponibile:**<br/> No </li> <li> **Variabile Riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> N/D </li> <li> **Dati contestuali:**<br/> </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Fotogrammi rilasciati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> dropFrames </li> <li> **Chiave API:**<br/> media.qoe.dropFrames </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 3 </li><li> **Descrizione:**<br/> il numero di fotogrammi saltati (Int). Questo valore viene calcolato come somma di tutti i fotogrammi saltati durante una sessione di riproduzione. Questo valore viene ricavato dall’ultimo valore di (l:stream:drop_frame).  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>dropFrameCount) </li> <li> **Heartbeat:**<br/> (l:stream:<br/>drop_frame) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile Riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> sull&#39;HIT </li> <li> **Nome Rapporto:**<br/> Fotogrammi Rilasciati </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>dropFrameCount) </li> <li> **Feed di dati:**<br/> videoqoedroppedframecountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>dropFrameCount) </li> </ul> |



### Eventi buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 2 </li><li> **Descrizione:**<br/> il numero di eventi del buffer. Questa metrica viene calcolata come un conteggio dei diversi stati del buffer che si sono verificati durante una sessione di riproduzione. Si tratta del numero di volte in cui il lettore entra in uno stato di buffer da altri stati, ad esempio la riproduzione o la pausa.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile Riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> sull&#39;HIT </li> <li> **Nome Rapporto:Eventi**<br/> Buffer </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **Feed dati:**<br/> videoqoebuffercountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### Durata totale buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** </li> <li> **Valore Di Esempio:**<br/> 30 </li><li> **Descrizione:**<br/> il tempo totale, in secondi, impiegato nel buffer. Questo valore viene calcolato come somma di tutte le durate degli eventi buffer che si sono verificati durante una sessione di riproduzione. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in  Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi. <br/>**Data di rilascio: 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **Heartbeat:**<br/> (l:event:durata) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile Riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> sull&#39;HIT </li> <li> **Nome rapporto:Durata**<br/> totale buffer </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **Feed dati:**<br/> videoqoebuffertimevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



### Modifiche bitrate

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.qoe.bitrateChange </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 3 </li><li> **Descrizione:**<br/> il numero di modifiche del bitrate (Integer). Questo valore viene calcolato come somma di tutti gli eventi di modifica del bitrate che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile Riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> sull&#39;HIT </li> <li> **Nome Rapporto:Modifiche**<br/> Bitrate </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Feed di dati:**<br/> videoqoebitratechangecountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### Errori/Eventi di errore

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 1 </li><li> **Descrizione:**<br/> Numero di errori (Integer). Questo valore viene calcolato come somma di tutti gli eventi di errore che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile Riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> sull&#39;HIT </li> <li> **Nome Rapporto:**<br/> Errori </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **Feed dati:**<br/> videoqoeerrorcountevar </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



### ID errore SDK lettore

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/> gli ID di errore univoci generati dall’SDK del lettore. I clienti devono fornire i codici/ID di errore al momento dell&#39;implementazione tramite le API di errore fornite.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>playerSdkErrors) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile Riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> sull&#39;HIT </li> <li> **Nome rapporto:ID errore SDK**<br/> Player </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>playerSdkErrors) </li> <li> **Feed dati:**<br/> videoqoeplayersdkerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>playerSdkErrors) </li> </ul> |



### ID errore esterni

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/> gli ID di errore univoci da qualsiasi origine esterna, ad esempio, errori CDN. I clienti devono fornire i codici/ID di errore al momento dell&#39;implementazione tramite le API di errore fornite.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>externalErrors) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile Riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> sull&#39;HIT </li> <li> **Nome rapporto:ID errore**<br/> esterni </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>externalErrors) </li> <li> **Feed dati:**<br/> videoqoeextneralerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>externalErrors) </li> </ul> |



### ID errore Media SDK

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/> gli ID di errore univoci generati da Media SDK durante la riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>mediaSdkErrors) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile Riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> sull&#39;HIT </li> <li> **Nome Rapporto:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>mediaSdkErrors) </li> <li> **Feed di dati:**<br/> mediaqoeexternalerrors </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>mediaSdkErrors) </li> </ul><br/> |




### Fine sessione {#session-end}

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** 2.1 </li> <li> **Valore di esempio:**<br/> end </li><li> **Descrizione:**<br/> L’evento end indica che l’SDK sta inviando una chiamata di chiusura al backend. Alla ricezione di questo evento, il backend chiuderà la sessione per il video e non eseguirà ulteriori elaborazioni. <br/>Se il supporto è stato completato al 100%, questo verrà inviato dopo  `s:event:type=complete.` Consultate  [Completamento ](audio-video-parameters.md#content-complete) contenuto per le informazioni correlate. </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> (s:event:type=end) </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> N/D </li> <li> **Dati contestuali:**<br/> </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> </li> </ul> |



## Metriche di qualità {#quality-metrics}

### Ora di inizio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 30.000 </li><li> **Descrizione:**<br/> questo valore predefinito è zero se non viene impostato tramite l&#39;oggetto QoSObject. Questo valore viene impostato in millisecondi. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in  Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi. <br/>**Data di rilascio: 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **Heartbeat:**<br/> (l:stream:start_time) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Ora di inizio </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>timeToStart) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>timeToStart) </li> </ul> |



### Eventi buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [startTime](./quality-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 2 </li><li> **Descrizione:**<br/> il numero di eventi del buffer (Integer). Questa metrica viene calcolata come un conteggio degli eventi del buffer che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome Rapporto:Eventi**<br/> Buffer </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bufferCount) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferCount) </li> </ul> |



### Durata totale buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore Di Esempio:**<br/> 15 </li><li> **Descrizione:**<br/> l&#39;importo totale del tempo impiegato (secondi; integer). Questo valore viene calcolato come somma di tutte le durate degli eventi buffer che si sono verificati durante una sessione di riproduzione. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in  Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi. <br/>**Data di rilascio: 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **Heartbeat:**<br/> (l:event:durata) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:Durata**<br/> totale buffer </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bufferTime) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bufferTime) </li> </ul> |



### Modifiche bitrate

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> Evento </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/> &quot;3&quot; </li><li> **Descrizione:**<br/> il numero di modifiche del bitrate. Questo valore viene calcolato come somma di tutti gli eventi di modifica del bitrate che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome Rapporto:Modifiche**<br/> Bitrate </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bitrateChangeCount) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount) </li> </ul> |



### Errori

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 1 </li><li> **Descrizione:**<br/> il numero di errori che si sono verificati (Integer). Questo valore viene calcolato come somma di tutti gli eventi di errore che si sono verificati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome Rapporto:Eventi**<br/> Di Errore </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>errorCount) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>errorCount) </li> </ul> |



### Fotogrammi rilasciati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 1 </li><li> **Descrizione:**<br/> il numero di fotogrammi saltati (Integer). Questo valore viene calcolato come somma di tutti i fotogrammi saltati durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>dropFrameCount) </li> <li> **Heartbeat:**<br/> (l:stream:<br/>drop_frame) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome Rapporto:**<br/> Fotogrammi Rilasciati </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>dropFrameCount) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>dropFrameCount) </li> </ul> |



### Rilasci prima dell&#39;avvio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di volte in cui un utente ha abbandonato il video prima del suo avvio. Questa metrica è impostata su 1 solo se non è stato eseguito il rendering di alcun contenuto, indipendentemente dagli annunci.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>dropBeforeStart) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=aa_start) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Rilasci prima dell&#39;avvio </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>dropBeforeStart) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>dropBeforeStart) </li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Flussi interessati dal buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di flussi interessati dal buffering. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno un evento del buffer.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>buffer) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome Rapporto:Flussi interessati**<br/> dal buffer </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>buffer) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Flussi interessati dalle modifiche bitrate

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di flussi in cui si sono verificate le modifiche del bitrate. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno un evento di modifica del bitrate.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateChange) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome Rapporto:Flussi interessati dalle modifiche**<br/> bitrate </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bitrateChange) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateChange) </li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Bitrate medio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore Di Esempio:**<br/> 3200 </li><li> **Descrizione:**<br/> bitrate medio (in kbps, numero intero). Questa metrica viene calcolata come media ponderata di tutti i valori del bitrate relativi alla durata di riproduzione che si è verificata durante una sessione di riproduzione.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>bitrateAverage) </li> <li> **Heartbeat:**<br/> (l:stream:bitrate) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome Report:Bitrate**<br/> Medio </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>bitrateAverage) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>bitrateAverage) </li> </ul> |



### Flussi interessati dall&#39;errore

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di flussi in cui si è verificato un evento di errore (ovvero,  `trackError` è stato chiamato durante la sessione di riproduzione ed è stata generata una chiamata  `type=error` heartbeat). </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>error) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=error) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome Report:Flussi**<br/> Errori </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>error) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>error) </li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Flussi interessati da fotogrammi rilasciati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di flussi in cui i fotogrammi sono stati eliminati. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione è stato eliminato almeno un fotogramma.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>dropFrames) </li> <li> **Heartbeat:**<br/> (l:stream:<br/>drop_frame) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome Report:Flussi Interessati Da Fotogrammi**<br/> Rilasciati </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>dropFrames) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>dropFrames) </li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Stallo dei flussi interessati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5+ </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> il numero di flussi in cui si è verificato un evento in stallo. Questa metrica è impostata su 1 solo se durante la riproduzione si è verificato almeno un arresto. I clienti dovranno creare le proprie regole di elaborazione per avere il valore disponibile per il reporting.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>stall) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome Rapporto:**<br/> Personalizzato</li> <li> **Feed di dati:**<br/> N/D </li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>stall) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stall) </li> </ul><br/> |

>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Stallo degli eventi

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5+ </li> <li> **Valore campione:**<br/> &quot;3&quot; </li><li> **Descrizione:**<br/> il numero di volte in cui la riproduzione è stata bloccata durante una sessione di riproduzione. I clienti dovranno creare le proprie regole di elaborazione per avere il valore disponibile per il reporting.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>stallCount) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome Rapporto:**<br/> Personalizzato</li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>stallCount) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stallCount) </li> </ul><br/> |



### Durata totale dello stallo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:impostazione**<br/> automatica </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5+ </li> <li> **Valore Di Esempio:**<br/> 12 </li><li> **Descrizione:**<br/> Tempo totale (secondi; integer) la riproduzione è stata bloccata durante una sessione di riproduzione. I clienti dovranno creare le proprie regole di elaborazione per avere il valore disponibile per il reporting.  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.qoe.<br/>stallTime) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=stall) </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome Rapporto:**<br/> Personalizzato</li> <li> **Dati contestuali:**<br/> (a.media.qoe.<br/>stallTime) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.qoe.<br/>stallTime) </li> </ul> <br/> |



## API correlate {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
