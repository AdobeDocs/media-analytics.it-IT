---
title: 'Parametri per gli annunci '
description: “Scopri i parametri degli annunci, tra cui l’implementazione, la rete e le variabili di reporting per i dati video sugli annunci.”
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
exl-id: 949e86cb-d265-4836-8825-a06b87203b15
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: f296b2549bb49162d735f29718057b3b1bbec231
workflow-type: ht
source-wordcount: '1927'
ht-degree: 100%

---

# Parametri per gli annunci {#ad-parameters}

Questo argomento presenta un elenco di dati di annunci video, inclusi i valori dei dati contestuali, che Adobe raccoglie tramite variabili della soluzione.

Descrizione dei dati della tabella:

* **Implementazione:** informazioni su valori e requisiti di implementazione
   * *Chiave*: variabile, impostata manualmente nell’app o automaticamente dall’SDK di Adobe Media.
   * *Obbligatorio*: indica se il parametro è necessario per il tracciamento video di base.
   * *Tipo*: specifica il tipo di variabile da impostare, stringa o numero.
   * *Inviato con*: indica quando vengono inviati i dati: *Avvio elemento multimediale* è la chiamata di analisi inviata all’avvio dell’elemento multimediale, *Avvio annuncio* è la chiamata di analisi inviata all’avvio dell’annuncio e così via; le chiamate *Chiusura* sono le chiamate di analisi compilate inviate direttamente dal server heartbeat al server di analisi alla fine della sessione multimediale, dell’annuncio, del capitolo, ecc. Le chiamate di chiusura non sono disponibili nelle chiamate dei pacchetti di rete.
   * *Versione SDK min.*: indica la versione SDK necessaria per accedere al parametro.
   * *Valore di esempio*: fornisce un esempio di utilizzo comune delle variabili.
* **Parametri di rete:** visualizza i valori passati ai server Adobe Analytics o Heartbeat. Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate dagli SDK di Adobe Media.
* **Reporting:** informazioni su come visualizzare e analizzare i dati video.
   * *Disponibile*: indica se i dati sono disponibili nella generazione rapporti per impostazione predefinita (*Sì*) o se è necessaria la configurazione personalizzata (*Personalizzato*)
   * *Variabile riservata*: indica se i dati vengono acquisiti come evento, eVar, prop o classificazione in una variabile riservata.
   * *Nome del rapporto*: nome del rapporto Adobe Analytics per la variabile
   * *Dati contestuali*: nome dei dati contestuali di Adobe Analytics passati al server di generazione rapporti e utilizzati nelle regole di elaborazione.
   * *Feed di dati*: nome della colonna per la variabile trovata nei feed di dati Clickstream o Live Stream
   * *Audience Manager*: nome delle caratteristiche trovato in Adobe Audience Manager

>[!IMPORTANT]
>
>Non modificare i nomi delle classificazioni per le variabili elencate di seguito che sono
>descritte in Variabile di generazione rapporti/riservata come “classificazione”.
>Le classificazioni per i file multimediali vengono definite quando una suite di rapporti è abilitata per il tracciamento
>degli elementi multimediali. Di tanto in tanto, Adobe aggiunge nuove proprietà e, quando ciò si verifica,
>i clienti devono riabilitare le suite di rapporti per accedere alle nuove proprietà dei contenuti multimediali
>. Durante il processo di aggiornamento Adobe determina se
>le classificazioni vengono abilitate verificando i nomi delle variabili. Se una di esse
>manca, Adobe aggiunge di nuovo quelle mancanti.

## Dati annuncio video {#ad-video-data}

### ID annuncio

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.id </li> <li> **Obbligatorio:**<br/> sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> avvio annuncio, chiusura annuncio </li> <li> **Versione SDK min.:** qualsiasi  </li> <li> **Valore di esempio:**<br/> “2125” </li><li> **Descrizione:**<br/> ID dell’annuncio. Qualsiasi combinazione di numeri interi e/o lettere  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>name) </li> <li> **Heartbeat:**<br/> (s:asset:ad_id) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> alla visita </li> <li> **Nome rapporto:**<br/> annuncio </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>name) </li> <li> **Feed dati:**<br/> videoad </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.name) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.@id </li> </ul> |



### Posizione annuncio in pod

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.podPosition </li> <li> **Obbligatorio:**<br/> sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> avvio annuncio, chiusura annuncio </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio.**<br/> 1 </li><li> **Descrizione:**<br/> la posizione (indice) dell’annuncio all’interno dell’interruzione pubblicitaria principale. Il primo annuncio ha indice 0, il secondo 1 e così via.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Heartbeat:**<br/> (s:asset:pod_position) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome rapporto:**<br/> posizione annuncio nel pod </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Feed dati:**<br/> videoadinpod </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podPosition) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetViewDetails.index </li> </ul> |



### Lunghezza annuncio

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.length </li> <li> **Obbligatorio:**<br/> sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> avvio annuncio, chiusura annuncio </li> <li> **Versione SDK min.:** 1.5.1 </li> <li> **Valore di esempio:**<br/> “15”  </li><li> **Descrizione:**<br/> lunghezza dell’annuncio video in secondi.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>length) </li> <li> **Heartbeat:**<br/> (l:asset:ad_length) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar e classificazione </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome rapporto:**<br/> lunghezza annuncio e lunghezza annuncio (variabile) </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>length) </li> <li> **Feed dati:**<br/> videoadlength </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.length) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.xmpDM:duration </li> </ul> |



### Nome del lettore dell’annuncio

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.playerName </li> <li> **Obbligatorio:**<br/> sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> avvio annuncio, chiusura annuncio </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> “ruota libera” </li><li> **Descrizione:**<br/> nome del lettore responsabile del rendering dell’annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Heartbeat:**<br/> (s:sp:player_name) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome rapporto:**<br/> nome del lettore dell’annuncio </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Feed dati:**<br/> videoadplayername </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.playerName) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetViewDetails.playerName </li> </ul> |



### Nome interruzione annuncio

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.podFriendlyName </li> <li> **Obbligatorio:**<br/> SDK: sì; API: no. </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> avvio annuncio, chiusura annuncio </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> “pre-roll” </li><li> **Descrizione:**<br/> il nome descrittivo dell’interruzione annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Heartbeat:**<br/> (s:asset:pod_name) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> classificazione </li> <li> **Nome rapporto:**<br/> nome pod </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetViewDetails.adBreak.dc:title </li> </ul> |



### Indice di interruzione annuncio

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.podPosition </li> <li> **Obbligatorio:**<br/> sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> 1 </li><li> **Descrizione:**<br/> l’indice dell’interruzione dell’annuncio all’interno del contenuto a partire da 1. Questa proprietà viene utilizzata **solo** da Media SDK per generare l’ID pod.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponibile:**<br/> no </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> N/D </li> <li> **Dati contestuali:**<br/> </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetViewDetails.index </li> </ul> |



### Posizione interruzione annuncio

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.podSecond </li> <li> **Obbligatorio:**<br/> sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> avvio annuncio, chiusura annuncio </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> 90 </li><li> **Descrizione:**<br/> offset dell’interruzione dell’annuncio all’interno del contenuto, in secondi.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Heartbeat:**<br/> (l:asset:pod_offset) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> classificazione </li> <li> **Nome rapporto:**<br/> posizione pod </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podSecond) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetViewDetails.adBreak.offset </li> </ul> |



### ID interruzione annuncio

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> impostata automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> avvio annuncio, chiusura annuncio </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>pod) </li> <li> **Heartbeat:**<br/> (s:asset:pod_id) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome rapporto:**<br/> pod annuncio </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>pod) </li> <li> **Feed dati:**<br/> videoadpod </li> <li> **Audience Manager:**<br/> </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetViewDetails.adBreak.@id </li> </ul> |



### Nome annuncio

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.name </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> avvia annuncio, chiudi annuncio </li> <li> **Versione SDK min.:** 1.5.1 </li> <li> **Valore di esempio:**<br/> “Ford F-150” </li><li> **Descrizione:**<br/> nome descrittivo dell’annuncio.  Nella generazione rapporti, “Nome annuncio” è la classificazione e “Nome annuncio (variabile)” è l’eVar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Heartbeat:**<br/> (s:asset:ad_name) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar e classificazione </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome rapporto:**<br/> nome annuncio e nome annuncio (variabile) </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.friendlyName) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.dc:title </li> </ul> |



## Metadati annuncio standard {#standard-ad-metadata}

### Inserzionista

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> INSERZIONISTA </li> <li> **Chiave API:**<br/> media.ad.advertiser </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> avvio annuncio, chiusura annuncio </li> <li> **Versione SDK min.:** 1.5.7 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> azienda/marchio il cui prodotto è presentato nell’annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>advertiser) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome rapporto:**<br/> <i>Inserzionista </i> </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>advertiser) </li> <li> **Feed dati:**<br/> videoinserzionista </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.advertiser) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.advertiser </li> </ul> |



### ID campagna

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> CAMPAIGN_ID </li> <li> **Chiave API:**<br/> media.ad.campaignId </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> avvio annuncio, chiusura annuncio </li> <li> **Versione SDK min.:** 1.5.7 </li> <li> **Valore di esempio:**<br/> intero o nome (stringa).  </li><li> **Descrizione:**<br/> ID della campagna pubblicitaria.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>campaign) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.campaign) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome rapporto:**<br/> <i>ID campagna </i> </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>campaign) </li> <li> **Feed dati:**<br/> videocampaign </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.campaign) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.campaign </li> </ul> |



### ID creatività

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> CREATIVE_ID </li> <li> **Chiave API:**<br/> media.ad.creativeId </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> avvio annuncio, chiusura annuncio </li> <li> **Versione SDK min.:** 1.5.7 </li> <li> **Valore di esempio:**<br/> intero o nome (stringa).  </li><li> **Descrizione:**<br/> ID della creatività dell’annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creative) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.creative) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome rapporto:**<br/> <i>ID creatività </i> </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>creative) </li> <li> **Feed dati:**<br/> adclassificationcreative </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creative) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.creativeID </li> </ul> |



### ID sito

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> SITE_ID </li> <li> **Chiave API:**<br/> media.ad.siteId </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> avvio annuncio, chiusura annuncio </li> <li> **Versione SDK min.:** 1.5.7 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> ID del sito dell’annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>site) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.site) </li> </ul> | <ul> <li> **Disponibile:**<br/> <i>Usa regola di elaborazione personalizzata </i> </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome rapporto:**<br/> personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>site) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.site) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.siteID </li> </ul> |



### URL creatività

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> CREATIVE_URL </li> <li> **Chiave API:**<br/> media.ad.creativeURL </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> avvio annuncio, chiusura annuncio </li> <li> **Versione SDK min.:** 1.5.7 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> URL della creatività dell’annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **Disponibile:**<br/> <i>Usa regola di elaborazione personalizzata </i> </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome rapporto:**<br/> personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creativeURL) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.creativeURL </li> </ul> |



### ID posizionamento

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> PLACEMENT_ID </li> <li> **Chiave API:**<br/> media.ad.placementId </li> <li> **Obbligatorio:**<br/> no </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> avvio annuncio, chiusura annuncio </li> <li> **Versione SDK min.:** 1.5.7 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> ID posizionamento dell’annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>placement) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.ad.placement) </li> </ul> | <ul> <li> **Disponibile:**<br/> <i>Usa regola di elaborazione personalizzata </i> </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> all’hit </li> <li> **Nome rapporto:**<br/> personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>placement) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.placement) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.placementID </li> </ul> |




## Metriche annuncio {#ad-metrics}

### Avvio annuncio

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> impostata automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> avvio annuncio </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> numero di avvii degli annunci video.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>view) </li> <li> **Heartbeat:**<br/> (s:event:type=start)<br/> (s:asset:type=ad) </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> avvio annuncio </li> <li> **Feed dati:**<br/> N/D </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>view) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.view) </li> <li> **Percorso campo XDM:**<br/> advertising.starts.value > 0 => “TRUE” </li> </ul> |



### Annuncio completato

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> impostata automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiusura annuncio </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> numero di annunci video completati.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>complete) </li> <li> **Heartbeat:**<br/> (s:event:type=complete)<br/> (s:asset:type=ad)  </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> completamento annuncio </li> <li> **Feed dati:**<br/> N/D </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>complete) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.complete) </li> <li> **Percorso campo XDM:**<br/> advertising.completes.value > 0 => “TRUE” </li> </ul> |



### Tempo trascorso dell’annuncio

|   Implementazione   | Parametri di rete | Reporting |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> impostata automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> chiusura annuncio </li> <li> **Versione SDK min.:** qualsiasi </li> <li> **Valore di esempio:**<br/> 15 </li><li> **Descrizione:**<br/> la quantità totale di tempo, in secondi, trascorsa a guardare l’annuncio (ovvero, il numero di secondi riprodotti).  Il valore viene visualizzato nel formato orario (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi.  <br/>**Data di rilascio: 13/09/18**  **</li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponibile:**<br/> sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> tempo trascorso dell’annuncio </li> <li> **Feed dati:**<br/> N/D </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.timePlayed) </li> <li> **Percorso campo XDM:**<br/> advertising.timePlayed.value </li> </ul> |



## API correlate {#section_Related_APIs}

### API createAdObject:

* Android: [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS: [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position)
* JavaScript: [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### API createAdBreakObject:

* Android: [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS: [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript: [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### API MediaHeartbeatConfig:

* Android: [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS: [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript: [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)
