---
title: Parametri per gli annunci
description: '"Scopri i parametri degli annunci, tra cui l’implementazione, la rete e le variabili di reporting per i dati video sugli annunci."'
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
exl-id: 949e86cb-d265-4836-8825-a06b87203b15
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: f296b2549bb49162d735f29718057b3b1bbec231
workflow-type: tm+mt
source-wordcount: '1927'
ht-degree: 3%

---

# Parametri per gli annunci{#ad-parameters}

Questo argomento presenta un elenco di dati di annunci video, inclusi i valori dei dati contestuali, che l&#39;Adobe raccoglie tramite variabili della soluzione.

Descrizione dei dati della tabella:

* **Implementazione:** Informazioni su valori e requisiti di implementazione
   * *Chiave* - Variabile, impostata manualmente nell’app o automaticamente dall’SDK di Adobe Medium.
   * *Obbligatorio* - Indica se il parametro è necessario per il tracciamento video di base.
   * *Tipo* - Specifica il tipo di variabile da impostare, stringa o numero.
   * *Inviato con* - Indica quando i dati vengono inviati: *Media Start* è la chiamata di analytics inviata all&#39;avvio del supporto, *Inizio annuncio* è la chiamata di analytics inviata all’inizio dell’annuncio e così via; la *Chiudi* le chiamate sono le chiamate analytics compilate inviate direttamente dal server heartbeat al server analytics alla fine della sessione multimediale, o la fine dell&#39;annuncio, del capitolo, ecc. Le chiamate di chiusura non sono disponibili nelle chiamate dei pacchetti di rete.
   * *Min Versione SDK* - Indica la versione SDK necessaria per accedere al parametro .
   * *Valore di esempio* - Fornisce un esempio di utilizzo comune delle variabili.
* **Parametri di rete:** Visualizza i valori passati ai server Adobe Analytics o Heartbeat. Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate dagli SDK di Adobe Medium.
* **Generazione rapporti:** Informazioni su come visualizzare e analizzare i dati video.
   * *Disponibile* - Indica se i dati sono disponibili nel reporting per impostazione predefinita (*Sì*) o richiede la configurazione personalizzata (*Personalizzato*)
   * *Variabile riservata* - Indica se i dati vengono acquisiti come evento, eVar, prop o classificazione in una variabile riservata.
   * *Nome del rapporto* - Nome del report Adobe Analytics per la variabile
   * *Dati contestuali* - Nome dei dati contestuali di Adobe Analytics passati al server di reporting e utilizzati nelle regole di elaborazione.
   * *Feed di dati* - Nome della colonna per la variabile trovata nei feed di dati Clickstream o Live Stream
   * *Audience Manager* - Nome delle caratteristiche trovato in Adobe Audience Manager

>[!IMPORTANT]
>
>Non modificare i nomi delle classificazioni per le variabili elencate di seguito che sono
>descritto in Segnalazione/Variabile riservata come &quot;classificazione&quot;.
>Le classificazioni per i file multimediali vengono definite quando una suite di rapporti è abilitata per i file multimediali
>tracking. Di tanto in tanto, Adobe aggiunge nuove proprietà e, quando ciò si verifica,
>i clienti devono riabilitare le suite di rapporti per accedere ai nuovi contenuti multimediali
>proprietà. Durante l&#39;Adobe del processo di aggiornamento determina se il
>Le classificazioni vengono abilitate controllando i nomi delle variabili. Se uno dei
>mancano, l&#39;Adobe aggiunge di nuovo quelli mancanti.

## Dati video annuncio {#ad-video-data}

### ID annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.id </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** Qualsiasi  </li> <li> **Valore di esempio:**<br/> &quot;2125&quot; </li><li> **Descrizione:**<br/> ID dell’annuncio. (Qualsiasi combinazione di numeri interi e/o lettere)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>name) </li> <li> **Heartbeat:**<br/> s:asset:ad_id) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> In visita </li> <li> **Nome report:**<br/> Annuncio </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>nome) </li> <li> **Feed dati:**<br/> video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.name) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.@id </li> </ul> |



### Posizione annuncio nel contenitore

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.podPosition </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 1 </li><li> **Descrizione:**<br/> La posizione (indice) dell’annuncio all’interno dell’interruzione pubblicitaria principale. Il primo annuncio ha l&#39;indice 0, il secondo ha l&#39;indice 1, ecc.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Heartbeat:**<br/> s:asset:pod_position) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Posizione annuncio nel contenitore </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Feed dati:**<br/> videoadinpod </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podPosition) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetViewDetails.index </li> </ul> |



### Lunghezza annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.length </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** 1.5.1. </li> <li> **Valore di esempio:**<br/> &quot;15&quot;  </li><li> **Descrizione:**<br/> Lunghezza dell’annuncio video in secondi.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>length) </li> <li> **Heartbeat:**<br/> l:asset:ad_length) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar e classificazione </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Lunghezza annuncio e Lunghezza annuncio (variabile) </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>lunghezza) </li> <li> **Feed dati:**<br/> videoadlength </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.length) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.xmpDM:duration </li> </ul> |



### Nome del lettore pubblicitario

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.playerName </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> &quot;ruota libera&quot; </li><li> **Descrizione:**<br/> Nome del lettore responsabile del rendering dell&#39;annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Heartbeat:**<br/> s:sp:player_name) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Nome del lettore pubblicitario </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Feed dati:**<br/> videoadplayername </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.playerName) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetViewDetails.playerName </li> </ul> |



### Nome interruzione annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.poNomeAmichevole </li> <li> **Obbligatorio:**<br/> SDK: Sì; API: No. </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> &quot;pre-roll&quot; </li><li> **Descrizione:**<br/> Il nome descrittivo dell&#39;Ad Break.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Heartbeat:**<br/> s:asset:pod_name) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome report:**<br/> Nome Pod </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetViewDetails.adBreak.dc:title </li> </ul> |



### Indice di interruzione annunci

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [posizione](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.podPosition </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 1 </li><li> **Descrizione:**<br/> L&#39;indice dell&#39;interruzione pubblicitaria all&#39;interno del contenuto a partire da 1. Questa proprietà viene utilizzata **only** dall’SDK di Media per generare l’ID Pod.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponibile:**<br/> No </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome report:**<br/> N/D </li> <li> **Dati contestuali:**<br/> </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetViewDetails.index </li> </ul> |



### Posizione interruzione annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.podSecond </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 90 </li><li> **Descrizione:**<br/> Offset dell&#39;interruzione pubblicitaria all&#39;interno del contenuto, in secondi.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Heartbeat:**<br/> l:asset:pod_offset) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome report:**<br/> Posizione dell&#39;asta </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podSecond) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetViewDetails.adBreak.offset </li> </ul> |



### ID interruzione annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>pod) </li> <li> **Heartbeat:**<br/> s:asset:pod_id) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Ad Pod </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>pod) </li> <li> **Feed dati:**<br/> videoadpod </li> <li> **Audience Manager:**<br/> </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetViewDetails.adBreak.@id </li> </ul> |



### Nome annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.name </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** 1.5.1. </li> <li> **Valore di esempio:**<br/> &quot;Ford F-150&quot; </li><li> **Descrizione:**<br/> Nome descrittivo dell&#39;annuncio.  Nel rapporto, &quot;Nome annuncio&quot; è la classificazione e &quot;Nome annuncio (variabile)&quot; è l’eVar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Heartbeat:**<br/> s:asset:ad_name) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar e classificazione </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Nome annuncio e nome annuncio (variabile) </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.friendlyName) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.dc:title </li> </ul> |



## Metadati annuncio standard {#standard-ad-metadata}

### Inserzionista

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> INSERZIONISTA </li> <li> **Chiave API:**<br/> media.ad.advertiser </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> Azienda/marchio il cui prodotto è presentato nell’annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>inserzionista) </li> <li> **Heartbeat:**<br/> s:meta:<br/>a.media.ad.ad) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> <i>Inserzionista </i> </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>inserzionista) </li> <li> **Feed dati:**<br/> videoinserzionista </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.ad) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.advertiser </li> </ul> |



### ID campagna

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> CAMPAIGN_ID </li> <li> **Chiave API:**<br/> media.ad.cacampaignId </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> Intero o nome (stringa).  </li><li> **Descrizione:**<br/> ID della campagna pubblicitaria.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>campagna) </li> <li> **Heartbeat:**<br/> s:meta:<br/>a.media.ad.cacampaign) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> <i>ID campagna </i> </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>campagna) </li> <li> **Feed dati:**<br/> videocampagna </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.cacampaign) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.campaign </li> </ul> |



### ID creativo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> CREATIVE_ID </li> <li> **Chiave API:**<br/> media.ad.creativeId </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> Intero o nome (stringa).  </li><li> **Descrizione:**<br/> ID dell&#39;annuncio creativo.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creativo) </li> <li> **Heartbeat:**<br/> s:meta:<br/>a.media.ad.creative) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> <i>ID creativo </i> </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>creativo) </li> <li> **Feed dati:**<br/> adclassificazioni creative </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creative) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.creativeID </li> </ul> |



### ID sito

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> SITE_ID </li> <li> **Chiave API:**<br/> media.ad.siteId </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> ID del sito dell&#39;annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>sito) </li> <li> **Heartbeat:**<br/> s:meta:<br/>a.media.ad.site) </li> </ul> | <ul> <li> **Disponibile:**<br/> <i>Usa regola di elaborazione personalizzata </i> </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>sito) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.site) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.siteID </li> </ul> |



### URL creativo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> CREATIVE_URL </li> <li> **Chiave API:**<br/> media.ad.creativeURL </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> URL dell’annuncio creativo.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Heartbeat:**<br/> s:meta:<br/>a.media.ad.crativeURL) </li> </ul> | <ul> <li> **Disponibile:**<br/> <i>Usa regola di elaborazione personalizzata </i> </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.crativeURL) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.creativeURL </li> </ul> |



### ID posizionamento

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> PLACEMENT_ID </li> <li> **Chiave API:**<br/> media.ad.placementId </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> ID posizionamento dell’annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>posizionamento) </li> <li> **Heartbeat:**<br/> s:meta:<br/>a.media.ad.placement) </li> </ul> | <ul> <li> **Disponibile:**<br/> <i>Usa regola di elaborazione personalizzata </i> </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>posizionamento) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.placement) </li> <li> **Percorso campo XDM:**<br/> advertising.adAssetReference.placementID </li> </ul> |




## Metriche annunci {#ad-metrics}

### Inizio annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio annuncio </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> Numero di avvii degli annunci video.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>vista) </li> <li> **Heartbeat:**<br/>  s:event:type=start)<br/> s:asset:type=ad) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Inizio annunci </li> <li> **Feed dati:**<br/> N/D </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>vista) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.view) </li> <li> **Percorso campo XDM:**<br/> advertising.started.value > 0 => &quot;TRUE&quot; </li> </ul> |



### Annuncio completato

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiudi annuncio </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> Numero di annunci video completati.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>completato) </li> <li> **Heartbeat:**<br/> s:event:type=complete)<br/> s:asset:type=ad)  </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Completamento annuncio </li> <li> **Feed dati:**<br/> N/D </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>completato) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.complete) </li> <li> **Percorso campo XDM:**<br/> advertising.complete.value > 0 => &quot;TRUE&quot; </li> </ul> |



### Tempo annuncio trascorso

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiudi annuncio </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 15 </li><li> **Descrizione:**<br/> La quantità totale di tempo, in secondi, trascorso a guardare l’annuncio (ovvero, il numero di secondi riprodotti).  Il valore viene visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi.  <br/>**Data di rilascio: 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Tempo annuncio trascorso </li> <li> **Feed dati:**<br/> N/D </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.timePlayed) </li> <li> **Percorso campo XDM:**<br/> advertising.timePlayed.value </li> </ul> |



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
