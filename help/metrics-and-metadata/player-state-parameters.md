---
title: Parametri dello stato del lettore
description: '"Scopri i parametri di tracciamento dello stato del lettore per le proprietà a schermo intero, Chiudi didascalia, Disattiva audio e Immagine nell’immagine."'
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: cd51ed3a-fe37-41e9-8243-dfd9deb514c1
feature: Media Analytics, Variables
role: User, Admin, Data Engineer
source-git-commit: c53c97ce06a5a6e2e7d7b20ed06b097a29b71fcb
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 1%

---

# Parametri dello stato del lettore{#player-state-parameters}

Questo argomento presenta un elenco dei dati sullo stato del lettore che Adobe raccoglie tramite variabili della soluzione.

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
>Non modificare i nomi delle classificazioni per le variabili elencate di seguito descritte in Reporting/Riservato Variable come &quot;classificazione&quot;.\
>Le classificazioni per i file multimediali vengono definite quando una suite di rapporti è abilitata per il tracciamento dei contenuti multimediali. Di tanto in tanto, Adobe aggiunge nuove proprietà e, in questo caso, i clienti devono riabilitare le suite di rapporti per accedere alle nuove proprietà multimediali. Durante il processo di aggiornamento, l’Adobe determina se le classificazioni sono abilitate controllando i nomi delle variabili. Se manca qualcuno di questi, Adobe aggiunge di nuovo quelli mancanti.

## Proprietà stato lettore {#player-state-properties}

Le funzionalità di tracciamento dello stato del lettore possono essere collegate a un flusso audio o video. Le metriche di tracciamento dello stato del lettore standardizzate sono memorizzate come variabili di soluzione. Gli stati standard sono: fullScreen, muto, closeCaption, pictureInPicture e inFocus.

### Proprietà a schermo intero

#### Streams interessati dallo schermo intero

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK**<br/> Imposta automaticamente  </li> <li> **Chiave API**<br/> N/D </li> <li> **Obbligatorio**<br/> No </li> <li> **Tipo**<br/> numero </li> <li> **Inviato con**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK**<br/> 3,0</li> <li> **Valore di esempio**<br/> TRUE </li><li> **Descrizione**<br/> Il numero di flussi interessati dallo schermo intero. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato a schermo intero. <br/> **Importante** <br/> Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.States.fullscreen.set<br/></li> <li> **Heartbeat**<br/> N/D </li> </ul> | <ul> <li> **Disponibile**<br/> Sì </li> <li> **Variabile riservata**<br/> event </li> <li> **Nome del rapporto**<br/> Streams interessati dallo schermo intero </li> <li> **Dati contestuali**<br/> a.media.States.fullscreen.set<br/> </li> <li> **Feed di dati**<br/> videostatefullscreen </li> <li> **Audience Manager**<br/> c_contextdata.a.media.States.fullscreen.set </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateSet </li> </ul> |

#### Conteggi a schermo intero

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK**<br/> Imposta automaticamente  </li> <li> **Chiave API**<br/> N/D </li> <li> **Obbligatorio**<br/> No </li> <li> **Tipo**<br/> numero </li> <li> **Inviato con**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK**<br/> 3,0</li> <li> **Valore di esempio**<br/> TRUE </li><li> **Descrizione**<br/> Numero di volte in cui è stato visualizzato uno schermo intero. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato a schermo intero. <br/> **Importante**<br/> Se questo evento è impostato, il conteggio è uguale al numero di volte in cui il video era nello stato a schermo intero. Se questo evento non è impostato, non viene inviato alcun valore.</li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.States.fullscreen.count<br/></li> <li> **Heartbeat**<br/> N/D </li> </ul> | <ul> <li> **Disponibile**<br/> Sì </li> <li> **Variabile riservata**<br/> event </li> <li> **Nome del rapporto**<br/> Conteggio a schermo intero </li> <li> **Dati contestuali**<br/> a.media.States.fullscreen.count<br/> </li> <li> **Feed di dati**<br/> videostatefullscreencount </li> <li> **Audience Manager**<br/> c_contextdata.media.States.fullscreen.count </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateCount </li> </ul> |



#### Durata totale schermo intero

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK**<br/> Imposta automaticamente  </li> <li> **Chiave API**<br/> N/D </li> <li> **Obbligatorio**<br/> No </li> <li> **Tipo**<br/> numero </li> <li> **Inviato con**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK**<br/> 3,0</li> <li> **Valore di esempio**<br/> TRUE </li><li> **Descrizione**<br/> Tempo di visualizzazione di uno schermo intero. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato a schermo intero. <br/> **Importante**<br/>  Se questo evento è impostato, l&#39;ora è uguale a quanto tempo il video era nello stato a schermo intero. Se questo evento non è impostato, non viene inviato alcun valore.  </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.States.fullscreen.time<br/></li> <li> **Heartbeat**<br/> N/D </li> </ul> | <ul> <li> **Disponibile**<br/> Sì </li> <li> **Variabile riservata**<br/> event </li> <li> **Nome del rapporto**<br/> Durata totale schermo intero </li> <li> **Dati contestuali**<br/> a.media.States.fullscreen.time<br/> </li> <li> **Feed di dati**<br/> videostatefullscreentime </li> <li> **Audience Manager**<br/> c_contextdata.media.States.fullscreen.time </li> <li> **Percorso campo XDM:**<br/>  media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateTime </li> </ul> |


### Chiudi proprietà didascalia

#### Streams interessati dai sottotitoli

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK**<br/> Imposta automaticamente  </li> <li> **Chiave API**<br/> N/D </li> <li> **Obbligatorio**<br/> No </li> <li> **Tipo**<br/> numero </li> <li> **Inviato con**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK**<br/> 3,0</li> <li> **Valore di esempio**<br/> TRUE </li><li> **Descrizione**<br/> Il numero di flussi interessati dalla funzione Sottotitoli. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato dei sottotitoli codificati. <br/> **Importante** <br/>  Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.States.closedcaptioning.set<br/></li> <li> **Heartbeat**<br/> N/D </li> </ul> | <ul> <li> **Disponibile**<br/> Sì </li> <li> **Variabile riservata**<br/> event </li> <li> **Nome del rapporto**<br/> Streams interessati dai sottotitoli </li> <li> **Dati contestuali**<br/> a.media.States.closedcaptioning.set<br/> </li> <li> **Feed di dati**<br/> videostateclosedcaptioning </li> <li> **Audience Manager**<br/> c_contextdata.a.media.States.closedcaptioning.set </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateSet </li> </ul> |


#### Conteggi per sottotitoli

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK**<br/> Imposta automaticamente  </li> <li> **Chiave API**<br/> N/D </li> <li> **Obbligatorio**<br/> No </li> <li> **Tipo**<br/> numero </li> <li> **Inviato con**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK**<br/> 3,0</li> <li> **Valore di esempio**<br/> TRUE </li><li> **Descrizione**<br/> Numero di volte in cui è stato visualizzato il sottotitolo chiuso . Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato di sottotitoli codificati. <br/> **Importante**<br/>  Se questo evento è impostato, il conteggio è uguale al numero di volte in cui il video era nello stato dei sottotitoli. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.States.closedcaptioning.count<br/></li> <li> **Heartbeat**<br/> N/D </li> </ul> | <ul> <li> **Disponibile**<br/> Sì </li> <li> **Variabile riservata**<br/> event </li> <li> **Nome del rapporto**<br/> Conteggio sottotitoli </li> <li> **Dati contestuali**<br/> a.media.States.closedcaptioning.count<br/> </li> <li> **Feed di dati**<br/> videostateclosedcaptioncount </li> <li> **Audience Manager**<br/> c_contextdata.media.States.closedcaptioning.count </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateCount </li> </ul> |


#### Durata totale sottotitoli

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK**<br/> Imposta automaticamente  </li> <li> **Chiave API**<br/> N/D </li> <li> **Obbligatorio**<br/> No </li> <li> **Tipo**<br/> numero </li> <li> **Inviato con**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK**<br/> 3,0</li> <li> **Valore di esempio**<br/> TRUE </li><li> **Descrizione**<br/>&#x200B;È stato visualizzato il periodo di tempo durante il quale venivano visualizzati i sottotitoli. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato a schermo intero. <br/> **Importante**<br/>  Se questo evento è impostato, l’ora è uguale a quanto tempo il video era nello stato dei sottotitoli. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.States.closedcaptioning.time<br/></li> <li> **Heartbeat**<br/> N/D </li> </ul> | <ul> <li> **Disponibile**<br/> Sì </li> <li> **Variabile riservata**<br/> event </li> <li> **Nome del rapporto**<br/> Durata totale sottotitoli </li> <li> **Dati contestuali**<br/> a.media.States.closedcaptioning.time<br/> </li> <li> **Feed di dati**<br/> videostateclosedcaptiontime </li> <li> **Audience Manager**<br/> c_contextdata.media.States.closedcaptioning.time </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateTime </li> </ul> |


### Proprietà disattivazione audio

#### Streams interessati dall&#39;audio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK**<br/> Imposta automaticamente  </li> <li> **Chiave API**<br/> N/D </li> <li> **Obbligatorio**<br/> No </li> <li> **Tipo**<br/> numero </li> <li> **Inviato con**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK**<br/> 3,0</li> <li> **Valore di esempio**<br/> TRUE </li><li> **Descrizione**<br/> Numero di flussi interessati da Muto. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato di disattivazione audio. <br/> **Importante** <br/> Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.States.mute.set<br/></li> <li> **Heartbeat**<br/> N/D </li> </ul> | <ul> <li> **Disponibile**<br/> Sì </li> <li> **Variabile riservata**<br/> event </li> <li> **Nome del rapporto**<br/> Streams interessati dall&#39;audio </li> <li> **Dati contestuali**<br/> a.media.States.mute.set<br/> </li> <li> **Feed di dati**<br/> video statemute </li> <li> **Audience Manager**<br/> c_contextdata.a.media.States.mute.set </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.mute.playerStateSet </li> </ul> |

#### Conteggi disattivati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK**<br/> Imposta automaticamente  </li> <li> **Chiave API**<br/> N/D </li> <li> **Obbligatorio**<br/> No </li> <li> **Tipo**<br/> numero </li> <li> **Inviato con**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK**<br/> 3,0</li> <li> **Valore di esempio**<br/> TRUE </li><li> **Descrizione**<br/>&#x200B;È stato visualizzato il numero di volte in cui è stato visualizzato l&#39;audio disattivato. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato di disattivazione audio. <br/> **Importante**<br/>  Se questo evento è impostato, il conteggio è uguale al numero di volte in cui il video era in stato Muto. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.States.mute.count<br/></li> <li> **Heartbeat**<br/> N/D </li> </ul> | <ul> <li> **Disponibile**<br/> Sì </li> <li> **Variabile riservata**<br/> event </li> <li> **Nome del rapporto**<br/> Conteggio audio </li> <li> **Dati contestuali**<br/> a.media.States.mute.count<br/> </li> <li> **Feed di dati**<br/> videostatemutecount </li> <li> **Audience Manager**<br/> c_contextdata.media.States.mute.count </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.mute.playerStateCount </li> </ul> |

#### Durata totale disattivazione

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK**<br/> Imposta automaticamente  </li> <li> **Chiave API**<br/> N/D </li> <li> **Obbligatorio**<br/> No </li> <li> **Tipo**<br/> numero </li> <li> **Inviato con**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK**<br/> 3,0</li> <li> **Valore di esempio**<br/> TRUE </li><li> **Descrizione**<br/>&#x200B;È stato visualizzato il periodo di disattivazione audio. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato di disattivazione audio. <br/> **Importante**<br/> Se questo evento è impostato, l&#39;ora è uguale a quanto tempo il video era in stato Muto. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.States.mute.time<br/></li> <li> **Heartbeat**<br/> N/D </li> </ul> | <ul> <li> **Disponibile**<br/> Sì </li> <li> **Variabile riservata**<br/> event </li> <li> **Nome del rapporto**<br/> Durata totale disattivazione </li> <li> **Dati contestuali**<br/> a.media.States.mute.time<br/> </li> <li> **Feed di dati**<br/> videostatemutetime </li> <li> **Audience Manager**<br/> c_contextdata.media.States.mute.time </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.mute.playerStateTime </li> </ul> |


### Proprietà immagine


#### Streams interessati da Picture in Picture

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK**<br/> Imposta automaticamente  </li> <li> **Chiave API**<br/> N/D </li> <li> **Obbligatorio**<br/> No </li> <li> **Tipo**<br/> numero </li> <li> **Inviato con**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK**<br/> 3,0</li> <li> **Valore di esempio**<br/> TRUE </li><li> **Descrizione**<br/> Il numero di flussi interessati da Picture in Picture. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato immagine nell&#39;immagine. <br/> **Importante** <br/> Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.States.pictureinpicture.set<br/></li> <li> **Heartbeat**<br/> N/D </li> </ul> | <ul> <li> **Disponibile**<br/> Sì </li> <li> **Variabile riservata**<br/> event </li> <li> **Nome del rapporto**<br/> Streams interessati da Picture in Picture </li> <li> **Dati contestuali**<br/> a.media.States.pictureinpicture.set<br/> </li> <li> **Feed di dati**<br/> video statepictureinpicture </li> <li> **Audience Manager**<br/> c_contextdata.a.media.States.pictureinpicture.set </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateSet </li> </ul> |


#### Conteggio immagini

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK**<br/> Imposta automaticamente  </li> <li> **Chiave API**<br/> N/D </li> <li> **Obbligatorio**<br/> No </li> <li> **Tipo**<br/> numero </li> <li> **Inviato con**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK**<br/> 3,0</li> <li> **Valore di esempio**<br/> TRUE </li><li> **Descrizione**<br/> Numero di volte in cui è stato visualizzato Picture in Picture. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato immagine nell&#39;immagine. <br/> **Importante** <br/> Se questo evento è impostato, il conteggio è uguale al numero di volte in cui il video era nello stato Picture in Picture. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.States.pictureinpicture.count<br/></li> <li> **Heartbeat**<br/> N/D </li> </ul> | <ul> <li> **Disponibile**<br/> Sì </li> <li> **Variabile riservata**<br/> event </li> <li> **Nome del rapporto**<br/> Conteggio immagini </li> <li> **Dati contestuali**<br/> a.media.States.pictureinpicture.count<br/> </li> <li> **Feed di dati**<br/> videostatepictureinpicturecount </li> <li> **Audience Manager**<br/> c_contextdata.media.States.pictureinpicture.count </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateCount </li> </ul> |


#### Durata totale immagine

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK**<br/> Imposta automaticamente  </li> <li> **Chiave API**<br/> N/D </li> <li> **Obbligatorio**<br/> No </li> <li> **Tipo**<br/> numero </li> <li> **Inviato con**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK**<br/> 3,0</li> <li> **Valore di esempio**<br/> TRUE </li><li> **Descrizione**<br/> Il periodo di tempo in cui è stato visualizzato Picture in Picture. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno stato immagine nell&#39;immagine. <br/> **Importante** <br/> Se questo evento è impostato, l&#39;ora è uguale a quanto tempo il video era nello stato Picture in Picture. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.States.pictureinpicture.time<br/></li> <li> **Heartbeat**<br/> N/D </li> </ul> | <ul> <li> **Disponibile**<br/> Sì </li> <li> **Variabile riservata**<br/> event </li> <li> **Nome del rapporto**<br/> Durata totale immagine </li> <li> **Dati contestuali**<br/> a.media.States.pictureinpicture.time<br/> </li> <li> **Feed di dati**<br/> videostatepictureinpitretime </li> <li> **Audience Manager**<br/> c_contextdata.media.States.pictureinpicture.time </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateTime </li> </ul> |


### In Proprietà dello stato attivo

#### Streams interessati da In Focus

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK**<br/> Imposta automaticamente  </li> <li> **Chiave API**<br/> N/D </li> <li> **Obbligatorio**<br/> No </li> <li> **Tipo**<br/> numero </li> <li> **Inviato con**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK**<br/> 3,0</li> <li> **Valore di esempio**<br/> TRUE </li><li> **Descrizione**<br/> Il numero di flussi interessati da In Focus. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno Stato attivo. <br/> **Importante** <br/> Se questo evento è impostato, l&#39;unico valore possibile è TRUE. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.States.infocus.set<br/></li> <li> **Heartbeat**<br/> N/D </li> </ul> | <ul> <li> **Disponibile**<br/> Sì </li> <li> **Variabile riservata**<br/> event </li> <li> **Nome del rapporto**<br/> Streams interessati da In Focus </li> <li> **Dati contestuali**<br/> a.media.States.infocus.set<br/> </li> <li> **Feed di dati**<br/> videostateinfocus </li> <li> **Audience Manager**<br/> c_contextdata.a.media.States.infocus.set </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateSet </li> </ul> |


#### Conteggi in focus

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK**<br/> Imposta automaticamente  </li> <li> **Chiave API**<br/> N/D </li> <li> **Obbligatorio**<br/> No </li> <li> **Tipo**<br/> numero </li> <li> **Inviato con**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK**<br/> 3,0</li> <li> **Valore di esempio**<br/> TRUE </li><li> **Descrizione**<br/>&#x200B;È stato visualizzato il numero di volte in cui è stato attivato il focus. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno Stato attivo. <br/> **Importante**<br/>  Se questo evento è impostato, il conteggio è uguale al numero di volte in cui il video si trovava nello stato In focus. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.States.infocus.count<br/></li> <li> **Heartbeat**<br/> N/D </li> </ul> | <ul> <li> **Disponibile**<br/> Sì </li> <li> **Variabile riservata**<br/> event </li> <li> **Nome del rapporto**<br/> Conteggio in focus </li> <li> **Dati contestuali**<br/> a.media.States.infocus.count<br/> </li> <li> **Feed di dati**<br/> videostateinfocuscount </li> <li> **Audience Manager**<br/> c_contextdata.media.States.infocus.count </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateCount </li> </ul> |


#### Durata totale messa a fuoco

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK**<br/> Imposta automaticamente  </li> <li> **Chiave API**<br/> N/D </li> <li> **Obbligatorio**<br/> No </li> <li> **Tipo**<br/> numero </li> <li> **Inviato con**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK**<br/> 3,0</li> <li> **Valore di esempio**<br/> TRUE </li><li> **Descrizione**<br/> Viene visualizzato il periodo di tempo in focus. Questa metrica è impostata su 1 solo se durante una sessione di riproduzione si è verificato almeno uno Stato attivo. <br/> **Importante** <br/> Se questo evento è impostato, l&#39;ora è uguale a quanto tempo il video era nello stato In focus. Se questo evento non è impostato, non viene inviato alcun valore.   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.States.infocus.time<br/></li> <li> **Heartbeat**<br/> N/D </li> </ul> | <ul> <li> **Disponibile**<br/> Sì </li> <li> **Variabile riservata**<br/> event </li> <li> **Nome del rapporto**<br/> Durata totale messa a fuoco </li> <li> **Dati contestuali**<br/> a.media.States.infocus.time<br/> </li> <li> **Feed di dati**<br/> videostateinfocustomime </li> <li> **Audience Manager**<br/> c_contextdata.media.States.infocus.time </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateTime </li> </ul> |


## API correlate {#related_apis_section}

* Android - [createStateObject](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* iOS - [createStateObjectWithName](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* Javascript - [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)
