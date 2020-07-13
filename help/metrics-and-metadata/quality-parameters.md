---
title: Parametri di qualità
description: null
uuid: 0d9fa764-edef-4178-8650-90c9a0852a57
translation-type: tm+mt
source-git-commit: cab9724476f7864ac23c4293e402e0443771cb1e
workflow-type: tm+mt
source-wordcount: '2984'
ht-degree: 2%

---


# Quality parameters{#quality-parameters}

Questo argomento presenta un elenco di dati sulla qualità dell&#39;esperienza (QoE/QoS), inclusi i valori dei dati contestuali, raccolti da Adobe tramite variabili della soluzione.

Descrizione dati tabella:

* **Implementazione:** Informazioni su valori e requisiti di implementazione
   * *Chiave* - Variabile, impostata manualmente nell’app o automaticamente dall’SDK di Adobe Media.
   * *Obbligatorio* - Indica se il parametro è richiesto per il tracciamento video di base.
   * *Tipo* - Specifica il tipo di variabile da impostare, stringa o numero.
   * *Inviato con* - Indica quando i dati vengono inviati: *Media Start* è la chiamata di analisi inviata all’avvio del supporto, *Ad Start* è la chiamata di analisi inviata all’avvio dell’annuncio e così via; le chiamate *Close* sono le chiamate di analisi compilate inviate direttamente dal server Heartbeat al server di analisi alla fine della sessione multimediale, o la fine dell&#39;annuncio, del capitolo, ecc. Le chiamate di chiusura non sono disponibili nelle chiamate dei pacchetti di rete.
   * *Min. Versione* SDK - Indica la versione SDK a cui sarà necessario accedere per il parametro.
   * *Valore* di esempio - Fornisce un esempio di utilizzo comune delle variabili.
* **Parametri di rete:** Visualizza i valori passati ai server Adobe  Analytics o Heartbeat. Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate dagli SDK di Adobe Media.
* **Reporting:** Informazioni su come visualizzare e analizzare i dati video.
   * *Disponibile* - Indica se i dati sono disponibili nei rapporti per impostazione predefinita (*Sì*) o richiedono una configurazione personalizzata (*Personalizzato*)
   * *Variabile* riservata - Indica se i dati vengono acquisiti come evento, eVar, prop o classificazione in una variabile riservata.
   * *Nome* report - Nome del report Adobe Analytics per la variabile
   * *Dati* contestuali - Nome dei dati contestuali di Adobe  Analytics passati al server di reporting e utilizzati nelle regole di elaborazione.
   * *Feed* dati - Nome colonna per la variabile trovata nei feed di dati Clickstream o Live Stream
   * *Audience Manager* - Nome caratteristica trovato in  Adobe Audience Manager

## Metadati qualità {#quality-metadata}

### Bitrate medio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/>media.qoe.bitrate</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Chiudi</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>800-899</li><li> **Descrizione:**<br/>bitrate medio (in kbps). Il valore è bucket predefiniti a intervalli di 100 kbps. Il bitrate medio è calcolato come media ponderata di tutti i valori del bitrate relativi alla durata di riproduzione che si è verificata durante una sessione di riproduzione.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>bitrateAverageBucket)</li> <li> **Battito cardiaco:**<br/>(l:stream:bitrate)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>eVar</li> <li> **Scadenza:**<br/>Su HIT</li> <li> **Nome rapporto:**<br/>Bitrate medio</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>bitrateAverageBucket)</li> <li> **Feed dati:**<br/>videoqoebitrateaverageevar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bitrateAverageBucket)</li> </ul> |


### Ora di inizio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/>media.qoe.timeToStart</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Inizio file multimediali, chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>30.000</li><li> **Descrizione:**<br/>questo valore predefinito è zero se non viene impostato tramite l&#39;oggetto QoSObject. Questo valore viene impostato in millisecondi. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in  Analysis Workspace e Reporting e  Analytics. Nelle API Feed dati, Data warehouse e Reporting i valori verranno visualizzati in secondi.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>timeToStart)</li> <li> **Battito cardiaco:**<br/>(l:stream:start_time)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>eVar</li> <li> **Scadenza:**<br/>Su HIT</li> <li> **Nome rapporto:**<br/>Ora di inizio</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>timeToStart)</li> <li> **Feed dati:**<br/>videoqetimetostartevar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>timeToStart)</li> </ul> |


### FPS

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/>media.qoe.framePerSecond</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Inizio file multimediali, chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>24</li><li> **Descrizione:**<br/>Il valore corrente del frame rate del flusso (in fotogrammi al secondo).</li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Battito cardiaco:**<br/>(l:stream:fps)</li> </ul> | <ul> <li> **Disponibile:**<br/>No</li> <li> **Variabile riservata:**<br/>N/D</li> <li> **Nome rapporto:**<br/>N/D</li> <li> **Dati contestuali:**<br/> </li> <li> **Feed dati:**<br/>N/D</li> <li> **Audience Manager:**<br/> </li> </ul> |



### Fotogrammi rilasciati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>dropFrames</li> <li> **Chiave API:**<br/>media.qoe.dropFrames</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>3</li><li> **Descrizione:**<br/>il numero di fotogrammi saltati (Int). Questo valore viene calcolato come somma di tutti i fotogrammi saltati durante una sessione di riproduzione. Questo valore viene ricavato dall’ultimo valore di (l:stream:drop_frame).</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>dropFrameCount)</li> <li> **Battito cardiaco:**<br/>(l:stream:<br/>drop_frame)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>eVar</li> <li> **Scadenza:**<br/>Su HIT</li> <li> **Nome rapporto:**<br/>Fotogrammi rilasciati</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>dropFrameCount)</li> <li> **Feed dati:**<br/>videoqoedroppedframecountevar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>dropFrameCount)</li> </ul> |



### Eventi buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/>N/D</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>2</li><li> **Descrizione:**<br/>il numero di eventi del buffer. Questa metrica viene calcolata come un conteggio dei diversi stati del buffer che si sono verificati durante una sessione di riproduzione. Si tratta del numero di volte in cui il lettore entra in uno stato di buffer da altri stati, ad esempio la riproduzione o la pausa.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>bufferCount)</li> <li> **Battito cardiaco:**<br/>(s:event:<br/>type=buffer)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>eVar</li> <li> **Scadenza:**<br/>Su HIT</li> <li> **Nome rapporto:**<br/>Eventi buffer</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>bufferCount)</li> <li> **Feed dati:**<br/>videoqoebuffercountevar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bufferCount)</li> </ul> |



### Durata totale buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/>N/D</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** </li> <li> **Valore campione:**<br/>30</li><li> **Descrizione:**<br/>il tempo totale, in secondi, impiegato nel buffer. Questo valore viene calcolato come somma di tutte le durate degli eventi buffer che si sono verificati durante una sessione di riproduzione. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in  Analysis Workspace e Reporting e  Analytics. Nelle API Feed dati, Data warehouse e Reporting i valori verranno visualizzati in secondi.<br/>**Data di rilascio: 13/09/18**</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>bufferTime)</li> <li> **Battito cardiaco:**<br/>(l:evento:durata)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>eVar</li> <li> **Scadenza:**<br/>Su HIT</li> <li> **Nome rapporto:**<br/>Durata totale buffer</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>bufferTime)</li> <li> **Feed dati:**<br/>videoqoebuffertimevar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bufferTime)</li> </ul> |



### Modifiche bitrate

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/>media.qoe.bitrateChange</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>3</li><li> **Descrizione:**<br/>il numero di modifiche del bitrate (Integer). Questo valore viene calcolato come somma di tutti gli eventi di modifica del bitrate che si sono verificati durante una sessione di riproduzione.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>bitrateChangeCount)</li> <li> **Battito cardiaco:**<br/>(s:event:<br/>type=bitrate_change)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>eVar</li> <li> **Scadenza:**<br/>Su HIT</li> <li> **Nome rapporto:**<br/>Modifiche bitrate</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>bitrateChangeCount)</li> <li> **Feed dati:**<br/>videoqoebitratechangecountevar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount)</li> </ul> |



### Errori/Eventi di errore

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> </li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>1</li><li> **Descrizione:**<br/>Numero di errori (Integer). Questo valore viene calcolato come somma di tutti gli eventi di errore che si sono verificati durante una sessione di riproduzione.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>errorCount)</li> <li> **Battito cardiaco:**<br/>(s:event:<br/>type=error)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>eVar</li> <li> **Scadenza:**<br/>Su HIT</li> <li> **Nome rapporto:**<br/>Errori</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>errorCount)</li> <li> **Feed dati:**<br/>videoqoeerrorcountevar</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>errorCount)</li> </ul> |



### ID errore SDK lettore

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/> </li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>gli ID di errore univoci generati dall’SDK del lettore. I clienti devono fornire i codici/ID di errore al momento dell&#39;implementazione tramite le API di errore fornite.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>playerSdkErrors)</li> <li> **Battito cardiaco:**<br/>(s:event:<br/>type=error)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>eVar</li> <li> **Scadenza:**<br/>Su HIT</li> <li> **Nome rapporto:**<br/>Errori</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>playerSdkErrors)</li> <li> **Feed dati:**<br/>videoqoeplayersderrori</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>playerSdkErrors)</li> </ul> |



### ID errore esterni

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/> </li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>gli ID di errore univoci da qualsiasi origine esterna, ad esempio, errori CDN. I clienti devono fornire i codici/ID di errore al momento dell&#39;implementazione tramite le API di errore fornite.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>externalErrors)</li> <li> **Battito cardiaco:**<br/>(s:event:<br/>type=error)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>eVar</li> <li> **Scadenza:**<br/>Su HIT</li> <li> **Nome rapporto:**<br/>Errori</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>externalErrors)</li> <li> **Feed dati:**<br/>videoqoeextneralerrori</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>externalErrors)</li> </ul> |



### ID errore Media SDK

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/> </li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>gli ID di errore univoci generati da Media SDK durante la riproduzione.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>mediaSdkErrors)</li> <li> **Battito cardiaco:**<br/>(s:event:<br/>type=error)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>eVar</li> <li> **Scadenza:**<br/>Su HIT</li> <li> **Nome rapporto:**<br/>Errori</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>mediaSdkErrors)</li> <li> **Feed dati:**<br/>mediaqoeesternalerrori</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>mediaSdkErrors)</li> </ul> |




### Fine sessione {#session-end}

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/> </li> <li> **Tipo:**<br/>string</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. SDK Version:** 2.1 </li> <li> **Valore campione:**<br/>end</li><li> **Descrizione:**<br/>L’evento end indica che l’SDK sta inviando una chiamata di chiusura al backend. Alla ricezione di questo evento, il backend chiuderà la sessione per il video e non eseguirà ulteriori elaborazioni.<br/>Se il supporto è stato completato al 100%, questo verrà inviato dopo`s:event:type=complete.`Consulta[Contenuto completo](audio-video-parameters.md#content-complete)per le informazioni correlate.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>N/D</li> <li> **Heartbeat:**<br/>(s:event:type=end)</li> </ul> | <ul> <li> **Disponibile:**<br/>Usa regola di elaborazione personalizzata</li> <li> **Variabile riservata:**<br/>event</li> <li> **Nome rapporto:**<br/>N/D</li> <li> **Dati contestuali:**<br/> </li> <li> **Feed dati:**<br/>N/D</li> <li> **Audience Manager:**<br/> </li> </ul> |



## Metriche di qualità {#quality-metrics}

### Ora di inizio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/>N/D</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>30.000</li><li> **Descrizione:**<br/>questo valore predefinito è zero se non viene impostato tramite l&#39;oggetto QoSObject. Questo valore viene impostato in millisecondi. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in  Analysis Workspace e Reporting e  Analytics. Nelle API Feed dati, Data warehouse e Reporting i valori verranno visualizzati in secondi.<br/>**Data di rilascio: 13/09/18**</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>timeToStart)</li> <li> **Battito cardiaco:**<br/>(l:stream:start_time)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>event</li> <li> **Nome rapporto:**<br/>Ora di inizio</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>timeToStart)</li> <li> **Feed dati:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>timeToStart)</li> </ul> |



### Eventi buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [startTime](./quality-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/>N/D</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>2</li><li> **Descrizione:**<br/>il numero di eventi del buffer (Integer). Questa metrica viene calcolata come un conteggio degli eventi del buffer che si sono verificati durante una sessione di riproduzione.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>bufferCount)</li> <li> **Battito cardiaco:**<br/>(s:event:<br/>type=buffer)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>event</li> <li> **Nome rapporto:**<br/>Eventi buffer</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>bufferCount)</li> <li> **Feed dati:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bufferCount)</li> </ul> |



### Durata totale buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/>N/D</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>15</li><li> **Descrizione:**<br/>l&#39;importo totale del tempo impiegato (secondi; integer). Questo valore viene calcolato come somma di tutte le durate degli eventi buffer che si sono verificati durante una sessione di riproduzione. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in  Analysis Workspace e Reporting e  Analytics. Nelle API Feed dati, Data warehouse e Reporting i valori verranno visualizzati in secondi.<br/>**Data di rilascio: 13/09/18**</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>bufferTime)</li> <li> **Battito cardiaco:**<br/>(l:evento:durata)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>event</li> <li> **Nome rapporto:**<br/>Durata totale buffer</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>bufferTime)</li> <li> **Feed dati:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bufferTime)</li> </ul> |



### Modifiche bitrate

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/>N/D</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>Evento</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>&quot;3&quot;</li><li> **Descrizione:**<br/>il numero di modifiche del bitrate. Questo valore viene calcolato come somma di tutti gli eventi di modifica del bitrate che si sono verificati durante una sessione di riproduzione.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>bitrateChangeCount)</li> <li> **Battito cardiaco:**<br/>(s:event:<br/>type=bitrate_change)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>event</li> <li> **Nome rapporto:**<br/>Modifiche bitrate</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>bitrateChangeCount)</li> <li> **Feed dati:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bitrateChangeCount)</li> </ul> |



### Errori

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/>N/D</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>1</li><li> **Descrizione:**<br/>il numero di errori che si sono verificati (Integer). Questo valore viene calcolato come somma di tutti gli eventi di errore che si sono verificati durante una sessione di riproduzione.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>errorCount)</li> <li> **Battito cardiaco:**<br/>(s:event:<br/>type=error)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>event</li> <li> **Nome rapporto:**<br/>Eventi errore</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>errorCount)</li> <li> **Feed dati:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>errorCount)</li> </ul> |



### Fotogrammi rilasciati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/>N/D</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>1</li><li> **Descrizione:**<br/>il numero di fotogrammi saltati (Integer). Questo valore viene calcolato come somma di tutti i fotogrammi saltati durante una sessione di riproduzione.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>dropFrameCount)</li> <li> **Battito cardiaco:**<br/>(l:stream:<br/>drop_frame)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>event</li> <li> **Nome rapporto:**<br/>Fotogrammi rilasciati</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>dropFrameCount)</li> <li> **Feed dati:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>dropFrameCount)</li> </ul> |



### Rilasci prima dell&#39;avvio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/>N/D</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>string</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>TRUE</li><li> **Descrizione:**<br/>il numero di volte in cui un utente ha abbandonato il video prima del suo avvio. Questa metrica è impostata su 1 solo se non è stato eseguito il rendering di alcun contenuto, indipendentemente dagli annunci.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>dropBeforeStart)</li> <li> **Battito cardiaco:**<br/>(s:event:<br/>type=aa_start)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>event</li> <li> **Nome rapporto:**<br/>Gocce prima dell&#39;inizio</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>dropBeforeStart)</li> <li> **Feed dati:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>dropBeforeStart)</li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Flussi interessati dal buffer

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/>N/D</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>string</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>TRUE</li><li> **Descrizione:**<br/>il numero di flussi interessati dal buffering. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno un evento del buffer.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>buffer)</li> <li> **Battito cardiaco:**<br/>(s:event:<br/>type=buffer)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>event</li> <li> **Nome rapporto:**<br/>Flussi interessati dal buffer</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>buffer)</li> <li> **Feed dati:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>buffer)</li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Flussi interessati dalle modifiche bitrate

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/>N/D</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>string</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>TRUE</li><li> **Descrizione:**<br/>il numero di flussi in cui si sono verificate le modifiche del bitrate. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno un evento di modifica del bitrate.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>bitrateChange)</li> <li> **Battito cardiaco:**<br/>(s:event:<br/>type=bitrate_change)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>event</li> <li> **Nome rapporto:**<br/>Flussi interessati dalle modifiche bitrate</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>bitrateChange)</li> <li> **Feed dati:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bitrateChange)</li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Bitrate medio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/>N/D</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>3200</li><li> **Descrizione:**<br/>bitrate medio (in kbps, numero intero). Questa metrica viene calcolata come media ponderata di tutti i valori del bitrate relativi alla durata di riproduzione che si è verificata durante una sessione di riproduzione.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>bitrateAverage)</li> <li> **Battito cardiaco:**<br/>(l:stream:bitrate)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>event</li> <li> **Nome rapporto:**<br/>Bitrate medio</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>bitrateAverage)</li> <li> **Feed dati:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>bitrateAverage)</li> </ul> |



### Flussi interessati dall&#39;errore

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/>N/D</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>string</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>TRUE</li><li> **Descrizione:**<br/>Il numero di flussi in cui si è verificato un evento di errore (ovvero,`trackError`è stato chiamato durante la sessione di riproduzione ed è stata generata una chiamata`type=error`heartbeat).</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>error)</li> <li> **Battito cardiaco:**<br/>(s:event:<br/>type=error)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>event</li> <li> **Nome rapporto:**<br/>Flussi interessati dall&#39;errore</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>error)</li> <li> **Feed dati:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>error)</li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Flussi interessati da fotogrammi rilasciati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/>N/D</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>string</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore campione:**<br/>TRUE</li><li> **Descrizione:**<br/>il numero di flussi in cui i fotogrammi sono stati eliminati. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione è stato eliminato almeno un fotogramma.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>dropFrames)</li> <li> **Battito cardiaco:**<br/>(l:stream:<br/>drop_frame)</li> </ul> | <ul> <li> **Disponibile:**<br/>Yes</li> <li> **Variabile riservata:**<br/>event</li> <li> **Nome rapporto:**<br/>Flussi interessati da fotogrammi rilasciati</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>dropFrames)</li> <li> **Feed dati:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>dropFrames)</li> </ul> |



>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Stallo dei flussi interessati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/>N/D</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>string</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. SDK Version:** 1.5+ </li> <li> **Valore campione:**<br/>TRUE</li><li> **Descrizione:**<br/>il numero di flussi in cui si è verificato un evento in stallo. Questa metrica è impostata su 1 solo se durante la riproduzione si è verificato almeno un arresto. I clienti dovranno creare le proprie regole di elaborazione per avere il valore disponibile per il reporting.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>stall)</li> <li> **Battito cardiaco:**<br/>(s:event:<br/>type=stall)</li> </ul> | <ul> <li> **Disponibile:**<br/>Usa regola di elaborazione personalizzata</li> <li> **Variabile riservata:**<br/>event</li> <li> **Nome rapporto:**<br/> </li> <li> **Feed dati:**<br/>N/D</li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>stall)</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>stall)</li> </ul> |

>[!IMPORTANT]
>
>Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.

### Stallo degli eventi

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/>N/D</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>string</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. SDK Version:** 1.5+ </li> <li> **Valore campione:**<br/>&quot;3&quot;</li><li> **Descrizione:**<br/>il numero di volte in cui la riproduzione è stata bloccata durante una sessione di riproduzione. I clienti dovranno creare le proprie regole di elaborazione per avere il valore disponibile per il reporting.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>stallCount)</li> <li> **Battito cardiaco:**<br/>(s:event:<br/>type=stall)</li> </ul> | <ul> <li> **Disponibile:**<br/>Usa regola di elaborazione personalizzata</li> <li> **Variabile riservata:**<br/>event</li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>stallCount)</li> <li> **Feed dati:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>stallCount)</li> </ul> |



### Durata totale dello stallo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>Imposta automaticamente</li> <li> **Chiave API:**<br/>N/D</li> <li> **Obbligatorio:**<br/>No</li> <li> **Tipo:**<br/>number</li> <li> **Inviato con:**<br/>Chiusura file multimediali</li> <li> **Min. SDK Version:** 1.5+ </li> <li> **Valore campione:**<br/>12</li><li> **Descrizione:**<br/>Tempo totale (secondi; integer) la riproduzione è stata bloccata durante una sessione di riproduzione. I clienti dovranno creare le proprie regole di elaborazione per avere il valore disponibile per il reporting.</li> </ul> | <ul> <li> **Adobe  Analytics:**<br/>(a.media.qoe.<br/>stallTime)</li> <li> **Battito cardiaco:**<br/>(s:event:<br/>type=stall)</li> </ul> | <ul> <li> **Disponibile:**<br/>Usa regola di elaborazione personalizzata</li> <li> **Variabile riservata:**<br/>event</li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/>(a.media.qoe.<br/>stallTime)</li> <li> **Feed dati:**<br/>N/D</li> <li> **Audience Manager:**<br/>(c_contextdata.<br/>a.media.qoe.<br/>stallTime)</li> </ul> |



## API correlate {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

