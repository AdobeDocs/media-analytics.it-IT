---
seo-title: Parametri annuncio
title: Parametri annuncio
uuid: 92 cd 7 f 97-bb 5 a -4 de 6-8946-453 d 30271 d 0 f
translation-type: tm+mt
source-git-commit: 180eafdfc536039820ade0b52e5c55f874719d8e

---


# Ad parameters{#ad-parameters}

Questo argomento presenta un elenco dei dati di annunci video, inclusi i valori dei dati contestuali, raccolti da Adobe tramite variabili della soluzione.

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

## Ad Video Data {#section_hq3_nbv_51b}

### ID annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [Adid](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.id </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi </li> <li> **Min. SDK Version:** Any  </li> <li> **Valore campione:**<br/> " 2125 " </li><li> **Descrizione:**<br/>ID dell'annuncio. (Qualsiasi combinazione di numero intero e/o lettere)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.na me) </li> <li> **Heartbeat:**<br/> (s: risorse: ad_ id) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> ALLA VISITA </li> <li> **Nome rapporto:**<br/> Annuncio </li> <li> **Dati contestuali:**<br/> (a.media.ad.na me) </li> <li> **Feed dati:**<br/> videoad </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.na me) </li> </ul> |



### Annuncio nella posizione contenitore

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.po Dposition </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> 1 </li><li> **Descrizione:**<br/>Posizione (indice) dell'annuncio all'interno dell'interruzione di annuncio principale. Il primo annuncio contiene index 0, il secondo ad indice 1, ecc.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.po Dposition) </li> <li> **Heartbeat:**<br/> (s: risorse: pod_ position) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Annuncio nella posizione contenitore </li> <li> **Dati contestuali:**<br/> (a.media.ad.po Dposition) </li> <li> **Feed dati:**<br/> videoadinpod </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.po Dposition) </li> </ul> |



### Lunghezza annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.le ngth </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi </li> <li> **Min. SDK Version:** 1.5.1 </li> <li> **Valore campione:**<br/> " 15 "  </li><li> **Descrizione:**<br/>Lunghezza del video, in secondi.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.le ngth) </li> <li> **Heartbeat:**<br/> (l: risorse: ad_ length) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar e classificazione </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Lunghezza annuncio e Lunghezza annuncio (variabile) </li> <li> **Dati contestuali:**<br/> (a.media.ad.le ngth) </li> <li> **Feed dati:**<br/> videoadlength </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.le ngth </li> </ul> |



### Nome lettore

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [Playername](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.pl Ayername </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> " Forma libera " </li><li> **Descrizione:**<br/>Nome del lettore responsabile del rendering dell'annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.pl Ayername) </li> <li> **Heartbeat:**<br/> (s: sp: player_ name) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Nome lettore </li> <li> **Dati contestuali:**<br/> (a.media.ad.pl Ayername) </li> <li> **Feed dati:**<br/> videoadplayername </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.pl Ayername </li> </ul> |



### Nome interruzione annunci

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.po Dfriendlyname </li> <li> **Richiesto:**<br/> SDK: Sì; API: No. </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> " pre-roll " </li><li> **Descrizione:**<br/>Il nome descrittivo dell'interruzione di annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.po Dfriendlyname) </li> <li> **Heartbeat:**<br/> (s: risorse: pod_ name) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Nome contenitore </li> <li> **Dati contestuali:**<br/> (a.media.ad.po Dfriendlyname) </li> <li> **Feed dati:**<br/> videoadpod </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.po Dfriendlyname) </li> </ul> |



### Indice interruzione annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.po Dposition </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> 1 </li><li> **Descrizione:**<br/>Indice dell'interruzione di annuncio all'interno del contenuto a partire da 1. This property is used **only** by the Media SDK to generate the Pod ID.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponibile:**<br/> No </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> N/D </li> <li> **Dati contestuali:**<br/> </li> <li> **Feed di dati:**<br/> </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Posizione interruzione annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [Starttime](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.po Dsecond </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> 90 </li><li> **Descrizione:**<br/>Offset dell'interruzione di annuncio all'interno del contenuto, in secondi.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.po Dsecond) </li> <li> **Heartbeat:**<br/> (l: risorse: pod_ offset) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Posizione contenitore </li> <li> **Dati contestuali:**<br/> (a.media.ad.po Dsecond) </li> <li> **Feed di dati:**<br/> </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.po Dsecond) </li> </ul> |



### ID interruzione annunci

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> c 4 a 577424 c 84067899 b 807 c 76722 d 495_ 1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.po d) </li> <li> **Heartbeat:**<br/> (l: risorse: pod_ id) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Ad pod </li> <li> **Dati contestuali:**<br/> (a.media.ad.po d) </li> <li> **Feed dati:**<br/> videoadpod </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Nome annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.na me </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi </li> <li> **Min. SDK Version:** 1.5.1 </li> <li> **Valore campione:**<br/> " Ford F -150 " </li><li> **Descrizione:**<br/>Nome descrittivo dell'annuncio. In reporting, «Ad Name» è la classificazione e «Ad Name (variable)» è la evar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.fr Iendlyname) </li> <li> **Heartbeat:**<br/> (s: risorse: ad_ name) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar e classificazione </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Nome annuncio e Nome annuncio (variabile) </li> <li> **Dati contestuali:**<br/> (a.media.ad.fr Iendlyname) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.fr Iendlyname) </li> </ul> |



## Standard Ad Metadata {#section_EFB805867916411E84DE1BA5A183D86A}

### Inserzionista

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> ADVERTISER </li> <li> **Chiave API:**<br/> media.ad.ad vertiser </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>Società/Marchio il cui prodotto è presentato nell'annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.ad vertiser) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.ad vertiser </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> <i>Inserzionista </i> </li> <li> **Dati contestuali:**<br/> (a.media.ad.ad vertiser) </li> <li> **Feed dati:**<br/> videoadvertiser </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.ad vertiser </li> </ul> |



### ID campagna

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> CAMPAIGN_ ID </li> <li> **Chiave API:**<br/> media.ad.ca Mpaignid </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore campione:**<br/> Integer, o nome (stringa).  </li><li> **Descrizione:**<br/>ID della campagna pubblicitaria.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.ca mpaign) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.ca mpaign </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> <i>ID campagna </i> </li> <li> **Dati contestuali:**<br/> (a.media.ad.ca mpaign) </li> <li> **Feed dati:**<br/> webampaign </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.ca mpaign </li> </ul> |



### ID creativo

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> CREATIVE_ ID </li> <li> **Chiave API:**<br/> media.ad.cr Eativeid </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore campione:**<br/> Integer, o nome (stringa).  </li><li> **Descrizione:**<br/>ID dell'annuncio creativo.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.cr eative) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.cr eative) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> <i>ID creativo </i> </li> <li> **Dati contestuali:**<br/> (a.media.ad.cr eative) </li> <li> **Feed dati:**<br/> adclassification ationcreative </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.cr eative) </li> </ul> |



### ID sito

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> SITE_ ID </li> <li> **Chiave API:**<br/> media.ad.si Teid </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>ID del sito di annunci.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.si te) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.si te) </li> </ul> | <ul> <li> **Disponibile:**<br/> <i>Utilizzare la regola di elaborazione personalizzata </i> </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> <i> </i> </li> <li> **Dati contestuali:**<br/> (a.media.ad.si te) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.si te) </li> </ul> |



### URL creativo

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> CREATIVE_ URL </li> <li> **Chiave API:**<br/> media.ad.cr Eativeurl </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>URL dell'annuncio creativo.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.cr Eativeurl) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.cr Eativeurl </li> </ul> | <ul> <li> **Disponibile:**<br/> <i>Utilizzare la regola di elaborazione personalizzata </i> </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> <i> </i> </li> <li> **Dati contestuali:**<br/> (a.media.ad.cr Eativeurl) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.cr Eativeurl </li> </ul> |



### ID posizionamento

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> PLACEMENT_ ID </li> <li> **Chiave API:**<br/> media.ad.pl Acementid </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>ID posizionamento dell'annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.pl acement) </li> <li> **Heartbeat:**<br/> (s: meta:<br/>a.media.ad.pl acement </li> </ul> | <ul> <li> **Disponibile:**<br/> <i>Utilizzare la regola di elaborazione personalizzata </i> </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> <i> </i> </li> <li> **Dati contestuali:**<br/> (a.media.ad.pl acement) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.pl acement </li> </ul> |




## Ad Metrics {#section_22AA1565F11C4F3990E2AB51CD3213F7}

### Inizio annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> TRUE </li><li> **Descrizione:**<br/>Inizia il numero di annunci video.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.vi ew) </li> <li> **Heartbeat:**<br/> (s: evento: type = start)<br/> (s: risorse: type = ad) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Annunci pubblicitari </li> <li> **Feed dati:**<br/> videoadstart </li> <li> **Dati contestuali:**<br/> (a.media.ad.vi ew) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.vi ew </li> </ul> |



### Annuncio completo

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Ad Close </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> TRUE </li><li> **Descrizione:**<br/>Numero di annunci video completati.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.com plll) </li> <li> **Heartbeat:**<br/> (s: evento: type = complete)<br/> (s: risorse: type = ad)  </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Annunci pubblicitari </li> <li> **Feed dati:**<br/> videoadcomplete </li> <li> **Dati contestuali:**<br/> (a.media.ad.com plll) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.com plug-up </li> </ul> |



### Tempo pubblicitario

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Ad Close </li> <li> **Min. SDK Version:** Any </li> <li> **Valore campione:**<br/> 15 </li><li> **Descrizione:**<br/>Il tempo totale, in secondi, trascorso guardando l'annuncio (ovvero, il numero di secondi trascorsi). Il valore verrà visualizzato nel formato temporale (HH: MM: SS) in Analysis Workspace e Reporting e analisi. In Feed dati, Data Warehouse e API di reporting i valori saranno visualizzati in secondi. <br/>**Data di rilascio: 09/13/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.ti Meplaying) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Tempo pubblicitario </li> <li> **Feed dati:**<br/> videoadtime </li> <li> **Dati contestuali:**<br/> (a.media.ad.ti Meplaying) </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.ad.ti Meplaying) </li> </ul> |



## Related APIs {#section_Related_APIs}

### API createadobject:

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### API createadbreakobject:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### API mediaheartbeatconfig:

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

