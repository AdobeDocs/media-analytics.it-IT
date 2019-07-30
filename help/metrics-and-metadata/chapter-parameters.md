---
seo-title: Parametri dei capitoli
title: Parametri dei capitoli
uuid: 2 a 6 b 9247-a 694-46 e 9-98 e 1-424 c 08 c 27 ec 2
translation-type: tm+mt
source-git-commit: af8da9da6cbe36e56f13cd7819f3682522e169bf

---


# Chapter parameters{#chapter-parameters}

Questo argomento presenta un elenco di dati relativi ai capitoli e/o ai segmenti, inclusi i valori dei dati contestuali, che Adobe raccoglie tramite variabili della soluzione.

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

>[!IMPORTANT]
>
>Non modificare i nomi delle classificazioni per tutte le variabili elencate di seguito, descritte in Reporting/Variabile riservata come "classificazione".\
>Le classificazioni multimediali vengono definite quando una suite di rapporti è abilitata per il tracciamento multimediale. Di tanto in tanto, Adobe aggiunge nuove proprietà e, in tal caso, i clienti devono riabilitare le suite di rapporti a ottenere l'accesso alle nuove proprietà del supporto. Durante il processo di aggiornamento Adobe determina se le classificazioni sono abilitate controllando i nomi delle variabili. Se mancano alcuni di essi, Adobe ne aggiunge di nuovo quelli mancanti.

## Chapter Metadata {#section_534D3A6BFEB24D1884F80AD6A50BF13C}

### Nome capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media. chapter. friendlyname </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio capitolo, Chiudi capitolo </li> <li> **Min. SDK Version:** 1.3 </li> <li> **Valore campione:**<br/> «The Big Bang Chapter 2 - Dating» </li><li> **Descrizione:**<br/>Nome del capitolo e/o del segmento.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. chapter.<br/>Friendlyname) </li> <li> **Heartbeat:**<br/> (s: stream: chapter_ name) </li> </ul> | <ul> <li> **Disponibile:**<br/> Creato per impostazione predefinita…  </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Nome capitolo </li> <li> **Dati contestuali:**<br/> (a. media. chapter.<br/>Friendlyname) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>Friendlyname) </li> </ul> |

### Posizione capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media. chapter. index </li> <li> **Richiesto:**<br/> SDK: No; API: Sì. </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi capitolo </li> <li> **Min. SDK Version:** 1.3 </li> <li> **Valore campione:**<br/> 2 </li><li> **Descrizione:**<br/>Posizione (indice, integer) del capitolo all'interno del contenuto.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. chapter.<br/>position) </li> <li> **Heartbeat:**<br/> (l: stream: chapter_ pos) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Posizione capitolo </li> <li> **Dati contestuali:**<br/> (a. media. chapter.<br/>position) </li> <li> **Feed di dati:**<br/> </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>position) </li> </ul> |

### Offset capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [Starttime](./chapter-parameters.md#related_apis_section) </li> <li> **Chiave API:**<br/> media. chapter. offset </li> <li> **Richiesto:**<br/> SDK: No; API: Sì. </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi capitolo </li> <li> **Min. SDK Version:** 1.3 </li> <li> **Valore campione:**<br/> 58 </li><li> **Descrizione:**<br/>L'offset del capitolo all'interno del contenuto (in secondi) dall'inizio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. chapter.<br/>offset) </li> <li> **Heartbeat:**<br/> (l: stream: chapter_ offset </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Offset capitolo </li> <li> **Dati contestuali:**<br/> (a. media. chapter.<br/>offset) </li> <li> **Feed di dati:**<br/> </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>offset) </li> </ul> |

### Lunghezza capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media. chapter. length </li> <li> **Richiesto:**<br/> SDK: No; API: Sì. </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi capitolo </li> <li> **Min. SDK Version:** 1.3 </li> <li> **Valore campione:**<br/> 486 </li><li> **Descrizione:**<br/>Lunghezza del capitolo, in secondi.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. chapter.<br/>length) </li> <li> **Heartbeat:**<br/> (l: stream: chapter_ length </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Lunghezza capitolo </li> <li> **Dati contestuali:**<br/> (a. media. chapter.<br/>length) </li> <li> **Feed di dati:**<br/> </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>length) </li> </ul> |

### Capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi capitolo </li> <li> **Min. SDK Version:** 1.3 </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>L'ID generato automaticamente del capitolo.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. chapter.<br/>name) </li> <li> **Heartbeat:**<br/> (s: stream: chapter_ id) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Capitolo </li> <li> **Dati contestuali:**<br/> (a. media. chapter.<br/>name) </li> <li> **Feed dati:**<br/> videocapitolo </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>name) </li> </ul> |

## Chapter Metrics {#section_1C47D6FB1DF343C39CE7A8F724406F33}

### Inizio capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico  </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio capitolo </li> <li> **Min. SDK Version:** 1.3 </li> <li> **Valore campione:**<br/> TRUE </li><li> **Descrizione:**<br/>Viene avviato il numero del capitolo. **Importante:** Se l'evento è impostato, l'unico valore possibile è TRUE. Se questo evento non viene impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. chapter.<br/>view) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = chapter_ start) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Inizio capitolo g </li> <li> **Dati contestuali:**<br/> (a. media. chapter.<br/>view) </li> <li> **Feed dati:**<br/> videochapterstart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>view) </li> </ul> |

### Completamento capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico  </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi capitolo </li> <li> **Min. SDK Version:** 1.3</li> <li> **Valore campione:**<br/> TRUE </li><li> **Descrizione:**<br/>Il numero di completamento del capitolo. **Importante:** Se l'evento è impostato, l'unico valore possibile è TRUE. Se questo evento non viene impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. chapter.<br/>completato) </li> <li> **Heartbeat:**<br/> (s: evento:<br/>type = chapter_ complete) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Completamento capitolo g </li> <li> **Dati contestuali:**<br/> (a. media. chapter.<br/>completato) </li> <li> **Feed dati:**<br/> videochaptercomplete </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>completato) </li> </ul> |

### Durata capitolo

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico  </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi capitolo </li> <li> **Min. SDK Version:** 1.3 </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>Il tempo trascorso sul capitolo. Il valore verrà visualizzato nel formato temporale (HH: MM: SS) in Analysis Workspace e Reporting e analisi. In Feed dati, Data Warehouse e API di reporting i valori saranno visualizzati in secondi. <br/>**Data di rilascio: 09/13/18**   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. chapter.<br/>Timeplayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Tempo capitolo impiegato g </li> <li> **Dati contestuali:**<br/> (a. media. chapter.<br/>Timeplayed) </li> <li> **Feed dati:**<br/> videochaptertime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. chapter.<br/>Timeplayed) </li> </ul> |

## Related APIs {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
