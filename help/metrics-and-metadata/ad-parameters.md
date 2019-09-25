---
seo-title: Parametri annuncio
title: Parametri annuncio
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
translation-type: tm+mt
source-git-commit: af8da9da6cbe36e56f13cd7819f3682522e169bf

---


# Parametri annuncio{#ad-parameters}

Questo argomento presenta un elenco di dati di annunci video, inclusi i valori dei dati contestuali, raccolti da Adobe tramite le variabili della soluzione.

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

>[!IMPORTANT]
>
>Non modificare i nomi delle classificazioni per le variabili elencate di seguito
>descritto in Segnalazione/Riservata Variabile come "classificazione".
>Le classificazioni dei supporti vengono definite quando una suite di rapporti è abilitata per i supporti
>tracking. Di tanto in tanto, Adobe aggiunge nuove proprietà e, quando ciò si verifica,
>i clienti devono riabilitare le loro suite di rapporti per poter accedere ai nuovi supporti
>proprietà. Durante il processo di aggiornamento, Adobe determina se la variabile
>Le classificazioni sono abilitate controllando i nomi delle variabili. Se uno dei
>se mancano, Adobe aggiunge di nuovo quelli mancanti.

## Aggiungi dati video {#section_hq3_nbv_51b}

### ID annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> ****<br/> Chiave API: media.ad.id </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio annuncio, Chiudi annuncio </li> <li> **Min.** Versione SDK: Qualsiasi  </li> <li> ****<br/> Valore campione: "2125" </li><li> **Descrizione:**<br/>ID dell’annuncio. (Qualsiasi combinazione di numeri interi e/o lettere)  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>name) </li> <li> ****<br/> Heartbeat: (s:asset:ad_id) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: In visita </li> <li> ****<br/> Nome rapporto: Annuncio </li> <li> ****<br/> Dati contestuali: (a.media.ad.<br/>name) </li> <li> ****<br/> Feed dati: videoad </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.name) </li> </ul> |



### Aggiungi in posizione contenitore

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> ****<br/> Chiave API: media.ad.podPosition </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Inizio annuncio, Chiudi annuncio </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: 1 </li><li> **Descrizione:**<br/>la posizione (indice) dell'annuncio all'interno dell'interruzione pubblicitaria principale. Il primo annuncio ha indice 0, il secondo annuncio ha indice 1, ecc.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>podPosition) </li> <li> ****<br/> Heartbeat: (s:asset:pod_position) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Aggiungi in posizione contenitore </li> <li> ****<br/> Dati contestuali: (a.media.ad.<br/>podPosition) </li> <li> ****<br/> Feed dati: videoadinpod </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### Lunghezza annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> ****<br/> Chiave API: media.ad.length </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Inizio annuncio, Chiudi annuncio </li> <li> **Min.** Versione SDK: 1.5.1 </li> <li> ****<br/> Valore campione: "15"  </li><li> **Descrizione:**<br/>Lunghezza del video annuncio in secondi.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>length) </li> <li> ****<br/> Heartbeat: (l:asset:ad_length) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar e classificazione </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto: Lunghezza annuncio e Lunghezza annuncio (variabile) </li> <li> ****<br/> Dati contestuali: (a.media.ad.<br/>length) </li> <li> ****<br/> Feed dati: videoadlength </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.length) </li> </ul> |



### Nome lettore annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> ****<br/> Chiave API: media.ad.playerName </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio annuncio, Chiudi annuncio </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: "ruota libera" </li><li> **Descrizione:**<br/>Nome del lettore responsabile del rendering dell'annuncio.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>playerName) </li> <li> ****<br/> Heartbeat: (s:sp:player_name) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Nome lettore annuncio </li> <li> ****<br/> Dati contestuali: (a.media.ad.<br/>playerName) </li> <li> ****<br/> Feed dati: videoadplayername </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### Nome interruzione annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> ****<br/> Chiave API: media.ad.poomeCordiale </li> <li> ****<br/> Obbligatorio: SDK: Sì; API: No. </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio annuncio, Chiudi annuncio </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: "pre-roll" </li><li> **Descrizione:**<br/>Il nome descrittivo dell'interruzione annuncio.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>podFriendlyName) </li> <li> ****<br/> Heartbeat: (s:asset:pod_name) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: Classificazione </li> <li> ****<br/> Nome rapporto: Nome contenitore </li> <li> ****<br/> Dati contestuali: (a.media.ad.<br/>podFriendlyName) </li> <li> ****<br/> Feed dati: videoadpod </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.poFriendlyName) </li> </ul> |



### Indice interruzione annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> ****<br/> Chiave API: media.ad.podPosition </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: number </li> <li> **Inviato con:**<br/> </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: 1 </li><li> **Descrizione:**<br/>l'indice dell'interruzione pubblicitaria all'interno del contenuto a partire da 1. Questa proprietà viene utilizzata **solo** da Media SDK per generare l’ID contenitore.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> ****<br/> Disponibile: No </li> <li> ****<br/> Variabile riservata: N/D </li> <li> ****<br/> Nome rapporto: N/D </li> <li> **Dati contestuali:**<br/> </li> <li> **Feed di dati:**<br/> </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Posizione interruzione annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> ****<br/> Chiave API: media.ad.podSecond </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Inizio annuncio, Chiudi annuncio </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: 90 </li><li> **Descrizione:**<br/>l'offset dell'interruzione annuncio all'interno del contenuto, in secondi.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>podSecond) </li> <li> ****<br/> Heartbeat: (l:asset:pod_offset) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: Classificazione </li> <li> ****<br/> Nome rapporto: Posizione contenitore </li> <li> ****<br/> Dati contestuali: (a.media.ad.<br/>podSecond) </li> <li> **Feed di dati:**<br/> </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### ID interruzione annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio annuncio, Chiudi annuncio </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>contenitore) </li> <li> ****<br/> Heartbeat: (s:asset:pod_id) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto: Ad Pod </li> <li> ****<br/> Dati contestuali: (a.media.ad.<br/>contenitore) </li> <li> ****<br/> Feed dati: videoadpod </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Nome annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> ****<br/> Chiave API: media.ad.na </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio annuncio, Chiudi annuncio </li> <li> **Min.** Versione SDK: 1.5.1 </li> <li> ****<br/> Valore campione: "Ford F-150" </li><li> **Descrizione:**<br/>Nome descrittivo dell'annuncio.  Nel reporting, "Ad Name" è la classificazione e "Ad Name (variabile)" è l'eVar.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>friendlyName) </li> <li> ****<br/> Heartbeat: (s:asset:ad_name) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar e classificazione </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto: Nome annuncio e nome annuncio (variabile) </li> <li> ****<br/> Dati contestuali: (a.media.ad.<br/>friendlyName) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## Metadati annuncio standard {#section_EFB805867916411E84DE1BA5A183D86A}

### Inserzionista

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: ADVERTISER </li> <li> ****<br/> Chiave API: media.ad.advertiser </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio annuncio, Chiudi annuncio </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>Azienda/Marchio il cui prodotto è presente nell'annuncio.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>advertiser) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> **Nome rapporto:**<br/> <i>Inserzionista </i> </li> <li> ****<br/> Dati contestuali: (a.media.ad.<br/>advertiser) </li> <li> ****<br/> Feed dati: videoadvertiser </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### ID campagna

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: CAMPAIGN_ID </li> <li> ****<br/> Chiave API: media.ad.capageId </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio annuncio, Chiudi annuncio </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore campione: Numero intero o nome (stringa).  </li><li> **Descrizione:**<br/>ID della campagna pubblicitaria.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>campaign) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.cacampaign) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> **Nome rapporto:**<br/> <i>ID campagna </i> </li> <li> ****<br/> Dati contestuali: (a.media.ad.<br/>campaign) </li> <li> ****<br/> Feed dati: video </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.campage) </li> </ul> |



### Creative ID

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: CREATIVE_ID </li> <li> ****<br/> Chiave API: media.ad.creativeId </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio annuncio, Chiudi annuncio </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore campione: Numero intero o nome (stringa).  </li><li> **Descrizione:**<br/>ID dell'annuncio creativo.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>creative) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.crative) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> **Nome rapporto:**<br/> <i>Creative ID </i> </li> <li> ****<br/> Dati contestuali: (a.media.ad.<br/>creative) </li> <li> ****<br/> Feed dati: adclassificationcreative </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.crative) </li> </ul> |



### ID sito

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: SITE_ID </li> <li> ****<br/> Chiave API: media.ad.siteId </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio annuncio, Chiudi annuncio </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>ID del sito dell'annuncio.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>sito) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.site) </li> </ul> | <ul> <li> **Disponibile:**<br/> <i>Usa regola di elaborazione personalizzata </i> </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> **Nome rapporto:**<br/> <i> </i> </li> <li> ****<br/> Dati contestuali: (a.media.ad.<br/>sito) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.si) </li> </ul> |



### URL creativo

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: CREATIVE_URL </li> <li> ****<br/> Chiave API: media.ad.creativeURL </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio annuncio, Chiudi annuncio </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:**<br/>URL dell'annuncio creativo.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>creativeURL) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.crativeURL) </li> </ul> | <ul> <li> **Disponibile:**<br/> <i>Usa regola di elaborazione personalizzata </i> </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> **Nome rapporto:**<br/> <i> </i> </li> <li> ****<br/> Dati contestuali: (a.media.ad.<br/>creativeURL) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.creativeURL) </li> </ul> |



### ID posizionamento

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: PLACEMENT_ID </li> <li> ****<br/> Chiave API: media.ad.placementId </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio annuncio, Chiudi annuncio </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> **Valore campione:**<br/> </li><li> **Descrizione:ID**<br/>posizionamento dell’annuncio.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>placement) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.ad.placement) </li> </ul> | <ul> <li> **Disponibile:**<br/> <i>Usa regola di elaborazione personalizzata </i> </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> **Nome rapporto:**<br/> <i> </i> </li> <li> ****<br/> Dati contestuali: (a.media.ad.<br/>placement) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.placement) </li> </ul> |




## Metriche annunci {#section_22AA1565F11C4F3990E2AB51CD3213F7}

### Inizio annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio annuncio </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: TRUE </li><li> **Descrizione:**<br/>numero di avvii di annunci video.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>view) </li> <li> ****<br/> Heartbeat:  (s:event:type=start)<br/> (s:asset:type=ad) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: event </li> <li> ****<br/> Nome rapporto: Inizio annuncio </li> <li> ****<br/> Feed dati: videoadstart </li> <li> ****<br/> Dati contestuali: (a.media.ad.<br/>view) </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.view) </li> </ul> |



### Annuncio completato

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Aggiungi chiusura </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: TRUE </li><li> **Descrizione:**<br/>numero di annunci video completati.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>completato) </li> <li> ****<br/> Heartbeat: (s:event:type=complete)<br/> (s:asset:type=ad)  </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto: Completamento annuncio </li> <li> ****<br/> Feed dati: videoadcomplete </li> <li> ****<br/> Dati contestuali: (a.media.ad.<br/>completato) </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.complete) </li> </ul> |



###  Tempo annuncio trascorso

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Aggiungi chiusura </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore campione: 15 </li><li> **Descrizione:**<br/>Il tempo totale, in secondi, trascorso a guardare l'annuncio (ovvero, il numero di secondi riprodotti).  Il valore verrà visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi.  <br/>**Data di rilascio: 13/09/18**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.ad.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: event </li> <li> ****<br/> Nome rapporto: Tempo annuncio trascorso </li> <li> ****<br/> Feed dati: videoadtime </li> <li> ****<br/> Dati contestuali: (a.media.ad.<br/>timePlayed) </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



## API correlate {#section_Related_APIs}

### API createAdObject:

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### API createAdBreakObject:

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### API MediaHeartbeatConfig:

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

