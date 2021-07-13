---
title: Parametri annuncio
description: '"Scopri i parametri degli annunci, tra cui l’implementazione, la rete e le variabili di reporting per i dati video sugli annunci."'
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
exl-id: 949e86cb-d265-4836-8825-a06b87203b15
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '1850'
ht-degree: 3%

---

# Parametri annuncio{#ad-parameters}

Questo argomento presenta un elenco di dati di annunci video, inclusi i valori dei dati contestuali, che l&#39;Adobe raccoglie tramite variabili della soluzione.

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
| <ul> <li> **Chiave SDK:**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.id </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** Qualsiasi  </li> <li> **Valore di esempio:**<br/> &quot;2125&quot; </li><li> **Descrizione:**<br/> ID dell’annuncio. (Qualsiasi combinazione di numeri interi e/o lettere)  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.ad.<br/>name) </li> <li> **Heartbeat:**<br/>  (:asset:triste_id) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> in visita </li> <li> **Nome rapporto:**<br/> Annuncio </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>nome) </li> <li> **Feed di dati:**<br/> video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.name) </li> </ul> |



### Posizione annuncio nel contenitore

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.podPosition </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 1 </li><li> **Descrizione:**<br/> la posizione (indice) dell’annuncio all’interno dell’interruzione pubblicitaria principale. Il primo annuncio ha l&#39;indice 0, il secondo ha l&#39;indice 1, ecc.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.ad.<br/>podPosition) </li> <li> **Heartbeat:**<br/>  (:asset:spod_position) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome del rapporto:**<br/> Aggiungi nella posizione del contenitore </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>podPosition) </li> <li> **Feed di dati:**<br/> video adinpod </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### Lunghezza annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.length </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** 1.5.1 </li> <li> **Valore di esempio:**<br/>  &quot;15&quot;  </li><li> **Descrizione:**<br/> Lunghezza dell’annuncio video in secondi.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.ad.<br/>length) </li> <li> **Heartbeat:**<br/>  (:asset:lad_length) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar e classificazione </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome rapporto:**<br/> Lunghezza annuncio e Lunghezza annuncio (variabile) </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>lunghezza) </li> <li> **Feed di dati:**<br/> videoadlength </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.length) </li> </ul> |



### Nome del lettore pubblicitario

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.playerName </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> &quot;FreeWheel&quot; </li><li> **Descrizione:**<br/> il nome del lettore responsabile del rendering dell’annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.ad.<br/>playerName) </li> <li> **Heartbeat:**<br/>  (nome_:sp:splayer) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome del rapporto:**<br/> Nome dell&#39;Ad Player </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>playerName) </li> <li> **Feed di dati:**<br/> videoadplayername </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### Nome interruzione annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.podFriendlyName </li> <li> **Obbligatorio:**<br/> SDK: Sì; API: No. </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/>  &quot;pre-roll&quot; </li><li> **Descrizione:**<br/> il nome descrittivo dell’interruzione annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.ad.<br/>podFriendlyName) </li> <li> **Heartbeat:**<br/>  (nome_:asset:spod) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Nome contenitore </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>podFriendlyName) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### Indice di interruzione annunci

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [posizione](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.podPosition </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 1 </li><li> **Descrizione:**<br/> l’indice dell’interruzione pubblicitaria all’interno del contenuto a partire da 1. Questa proprietà viene utilizzata **solo** dall&#39;SDK di Media per generare l&#39;ID Pod.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponibile:**<br/> No </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> N/D </li> <li> **Dati contestuali:**<br/> </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Posizione interruzione annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.podSecond </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 90 </li><li> **Descrizione:**<br/> l’offset dell’interruzione pubblicitaria all’interno del contenuto, in secondi.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.ad.<br/>podSecond) </li> <li> **Heartbeat:**<br/>  (:asset:lpod_offset) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Posizione contenitore </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>podSecond) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### ID interruzione annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore del campione:**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.ad.<br/>pod) </li> <li> **Heartbeat:**<br/>  (:asset:spod_id) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome rapporto:**<br/> Ad Pod </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>pod) </li> <li> **Feed di dati:**<br/> videoPod </li> <li> **Audience Manager:**<br/> </li> </ul> |



### Nome annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **Chiave API:**<br/> media.ad.name </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** 1.5.1 </li> <li> **Valore del campione:**<br/>  &quot;Ford F-150&quot; </li><li> **Descrizione:**<br/> Nome descrittivo dell’annuncio.  Nel rapporto, &quot;Nome annuncio&quot; è la classificazione e &quot;Nome annuncio (variabile)&quot; è l’eVar.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.ad.<br/>friendlyName) </li> <li> **Heartbeat:**<br/>  (nome_:asset:triste) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar e classificazione </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome rapporto:**<br/> Nome annuncio e nome annuncio (variabile) </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>friendlyName) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## Metadati annuncio standard {#standard-ad-metadata}

### Inserzionista

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> ADVERTISER </li> <li> **Chiave API:**<br/> media.ad.advertiser </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> azienda/marchio il cui prodotto è presentato nell’annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.ad.<br/>inserzionista) </li> <li> **Heartbeat:**<br/>  (:meta:<br/>sa.media.ad.advertiser) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome report:**<br/> <i>Inserzionista  </i> </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>inserzionista) </li> <li> **Feed di dati:**<br/> inserzionista video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.ad) </li> </ul> |



### ID campagna

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> CAMPAIGN_ID </li> <li> **Chiave API:**<br/> media.ad.cacampaignId </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> Integer o name (stringa).  </li><li> **Descrizione:**<br/> ID della campagna pubblicitaria.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.ad.<br/>campagna) </li> <li> **Heartbeat:**<br/>  (:meta:<br/>sa.media.ad.cacampaign) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome report:**<br/> <i>ID campagna </i> </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>campagna) </li> <li> **Feed di dati:**<br/> campagna di video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.cacampaign) </li> </ul> |



### ID creativo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> CREATIVE_ID </li> <li> **Chiave API:**<br/> media.ad.creativeId </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> Integer o name (stringa).  </li><li> **Descrizione:**<br/> ID dell’annuncio creativo.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.ad.<br/>creativo) </li> <li> **Heartbeat:**<br/>  (:meta:<br/>sa.media.ad.crativo) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome report:**<br/> <i>ID creativo  </i> </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>creativo) </li> <li> **Feed di dati:**<br/> classificazioni creative </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.creative) </li> </ul> |



### ID sito

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> SITE_ID </li> <li> **Chiave API:**<br/> media.ad.siteId </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> ID del sito dell’annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.ad.<br/>sito) </li> <li> **Heartbeat:**<br/>  (:meta:<br/>sa.media.ad.site) </li> </ul> | <ul> <li> **Disponibile:**<br/> <i>Usa regola di elaborazione personalizzata  </i> </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome rapporto:**<br/> personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>sito) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.site) </li> </ul> |



### URL creativo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> CREATIVE_URL </li> <li> **Chiave API:**<br/> media.ad.crativeURL </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> URL dell’annuncio creativo.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.ad.<br/>creativeURL) </li> <li> **Heartbeat:**<br/>  (:meta:<br/>sa.media.ad.crativeURL) </li> </ul> | <ul> <li> **Disponibile:**<br/> <i>Usa regola di elaborazione personalizzata  </i> </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome rapporto:**<br/> personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>creativeURL) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.crativeURL) </li> </ul> |



### ID posizionamento

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> PLACEMENT_ID </li> <li> **Chiave API:**<br/> media.ad.placementId </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio annuncio, Chiudi annuncio </li> <li> **Min Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> </li><li> **Descrizione:**<br/> ID posizionamento dell’annuncio.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.ad.<br/>posizionamento) </li> <li> **Heartbeat:**<br/>  (:meta:<br/>sa.media.ad.placement) </li> </ul> | <ul> <li> **Disponibile:**<br/> <i>Usa regola di elaborazione personalizzata  </i> </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> su HIT </li> <li> **Nome rapporto:**<br/> personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>posizionamento) </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.placement) </li> </ul> |




## Metriche annunci {#ad-metrics}

### Inizio annuncio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Ad Start </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> numero di avvii dell&#39;annuncio video.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.ad.<br/>vista) </li> <li> **Heartbeat:**<br/>  (:event:stype=start)<br/> (:asset:stype=ad) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Avvio annuncio </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>vista) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.view) </li> </ul> |



### Annuncio completato

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Aggiungi chiusura </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li><li> **Descrizione:**<br/> numero di annunci video completati.   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.ad.<br/>completato) </li> <li> **Heartbeat:**<br/> (:event:stype=complete)<br/> (:asset:stype=ad)  </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Completamento annuncio </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>completato) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.complete) </li> </ul> |



### Tempo annuncio trascorso

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Aggiungi chiusura </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 15 </li><li> **Descrizione:**<br/> la quantità totale di tempo, in secondi, trascorso a guardare l’annuncio (ovvero, il numero di secondi riprodotti).  Il valore verrà visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi.  <br/>**Data di rilascio: 13/09/18**  </li> </ul> | <ul> <li> **Adobe Analytics:**<br/>  (a.media.ad.<br/>timePlayed) </li> <li> **Heartbeat:**<br/> </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Tempo annuncio trascorso </li> <li> **Feed di dati:**<br/> N/D </li> <li> **Dati contestuali:**<br/> (a.media.ad.<br/>timePlayed) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



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
