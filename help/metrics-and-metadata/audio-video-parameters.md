---
seo-title: Parametri audio e video
title: Parametri audio e video
uuid: fdacfb 8 b-db 3 e -46 fb-b 9 ad-c 3 a 749555 b 2 a
translation-type: tm+mt
source-git-commit: af8da9da6cbe36e56f13cd7819f3682522e169bf

---


# Audio and video parameters{#audio-and-video-parameters}

>[!IMPORTANT]
>
>Il 7 febbraio 2019, Adobe Analytics per video e audio ha rilasciato un cambiamento di nome della metrica. <i>Media Initiates</i> verrà ora denominato <i>Media Starts</i>. Questa modifica è stata eseguita per riflettere gli standard di settore nelle metriche e nei report, e per rendere la metrica facilmente identificabile nei rapporti.

>[!NOTE]
>
>A partire dal 13 settembre 2018, è stata apportata una modifica alle etichette per alcune dimensioni, metriche e rapporti, per consentire il monitoraggio cross-content delle analisi video e audio. The labels that have been changed include: *video initiates* to *media initiates*, *video length* to *content length*, and *video name* to *content name*. I rapporti video in Reporting e analisi sono stati aggiornati per utilizzare il nome "File multimediali" anziché "Video". Le modifiche delle etichette non cambiavano la raccolta dati o dati storici. Prendi nota di queste modifiche nel caso in cui li usi in Generatore di report o in altri dati automatizzati esterni che potrebbero essere influenzati da questa modifica.

Questo argomento presenta un elenco di dati audio e video, compresi i valori dei dati contestuali, che Adobe raccoglie tramite variabili della soluzione.

Descrizione dati tabella:

* **Implementazione:** Informazioni sui valori e i requisiti di implementazione
   * *Chiave* - Variabile, impostata manualmente nell'app o automaticamente da Adobe Media SDK.
   * *Obbligatorio* - Indica se il parametro è obbligatorio per il tracciamento audio e video di base.
   * *Tipo* : specifica il tipo della variabile da impostare, stringa o numero.
   * *Inviato con* - Indica la data di invio dei dati: *Media Start* è la chiamata di analisi inviata sull'avvio dei supporti, *Ad Avvio* è la chiamata di analisi inviata all'avvio e così via. Le *chiamate Close* sono le chiamate di analisi compilate inviate direttamente dal server heartbeat al server di analisi alla fine della sessione multimediale, o alla fine dell'annuncio, del capitolo, ecc. Le chiamate close non sono disponibili nelle chiamate del pacchetto di rete.
   * *Min. SDK Version* - Indicates which SDK version you would need to access the parameter.
   * *Valore di esempio* - Fornisce esempi di utilizzo variabile delle variabili.
* **Parametri di rete:** Visualizza i valori passati ai server Adobe Analytics o Heartbeat. Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate da Adobe Media SDK.
* **Reporting:** Informazioni su come visualizzare e analizzare i dati audio e video.
   * *Disponibile* - Indica se i dati sono disponibili nel reporting per impostazione predefinita (*Yes*) o richiedono un set personalizzato (*personalizzato*)
   * *Variabile riservata* - Indica se i dati sono acquisiti come evento, evar, prop o classificati in una variabile riservata.
   * *Scadenza* : indica se i dati scadono dopo ogni hit o dopo ogni visita.
   * *Nome rapporto* - Nome del rapporto Adobe Aanlytics per la variabile
   * *Dati contestuali* - Nome dei dati contestuali di Adobe Analytics passati al server di reporting e utilizzati nelle regole di elaborazione.
   * *Feed dati* - Nome colonna per la variabile trovata nei feed dati Clickstream o Live Stream
   * *Audience Manager* - Nome caratteristica trovato in Adobe Audience Manager

>[!IMPORTANT]
>
>Non modificare i nomi delle classificazioni per tutte le variabili elencate di seguito, descritte in Reporting/Variabile riservata come "classificazione".\
>Le classificazioni multimediali vengono definite quando una suite di rapporti è abilitata per il tracciamento multimediale. Di tanto in tanto, Adobe aggiunge nuove proprietà e, in tal caso, i clienti devono riabilitare le suite di rapporti a ottenere l'accesso alle nuove proprietà del supporto. Durante il processo di aggiornamento Adobe determina se le classificazioni sono abilitate controllando i nomi delle variabili. Se mancano alcuni di essi, Adobe ne aggiunge di nuovo quelli mancanti.

## Core Audio and Video Data {#section_y55_y1m_n1b}

### Stream Type {#stream-type}

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [Streamtype](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media. streamtype </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 2.2 <br/><br/>Available in [Media Collection API Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> **Valore di esempio:**<br/> " video " </li> <li> **Descrizione:**<br/> Identifica il tipo di flusso. I valori validi sono "audio", "video" e "". <br/><br/>[Segmenti di reporting](/help/metrics-and-metadata/segments.md): <br/><br/>Tipo flusso media: Tutti - <br/>Segmentare tutti i dati del flusso multimediale; Regola: Content (ID) is <br/><br/>Media Stream Type: Audio - <br/>Segmentare tutti i dati del flusso audio; Regola: Content (ID) esiste AND Media Stream Type = Audio <br/><br/>Media Stream Type: " Video " - <br/>Segmento tutti i dati del flusso video; Regola: Content (ID) is AND Media Stream Type!= audio <br/><br/> **Data di rilascio: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. streamtype) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. streamtype) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> ALLA VISITA </li> <li> **Nome rapporto:**<br/> Contenuto </li> <li> **Dati contestuali:**<br/> (a. media. streamtype) </li> <li> **Feed dati:**<br/> videostreamtype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. streamtype) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [Mediaid](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media. id </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> " 4586695 ABC " </li> <li>**Descrizione:**<br/> ID contenuto del contenuto, che può essere utilizzato per tornare ad altri ID settori/CMS, pari all'ultimo valore di `s:asset:video_id.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. name) </li> <li> **Heartbeats:**<br/> (s: risorse: video_ id) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> ALLA VISITA </li> <li> **Nome rapporto:**<br/> Contenuto </li> <li> **Dati contestuali:**<br/> (a. media. name) </li> <li> **Feed dati:**<br/> video </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Lunghezza contenuto (variabile)

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media. length </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> VOD: 128; Live: 86400; Lineare: 1800. </li><li> **Descrizione:**<br/> Lunghezza/Fase di esecuzione delle clip - Questa è la lunghezza massima (o durata) del contenuto in uso (in secondi). It equals the last value of `l:asset:length` from events of type Main. <br/>Se `l:asset:length` non viene impostato, viene utilizzato l'ultimo `l:asset:duration` valore. <br/>Nei rapporti, Durata video è la classificazione e Lunghezza contenuto (variabile) è la evar. <br/> **Importante:** Questa proprietà viene utilizzata per calcolare diverse metriche, ad esempio metriche di tracciamento dell'avanzamento e Pubblico medio minuto. Se non è impostata, o non è maggiore di zero, queste metriche non sono disponibili. Per gli elementi multimediali live con durata sconosciuta, il valore predefinito è 86400. <br/>Pre versione `l:asset:duration`1.5.1: dopo 1.5.1, si tratta di `l:asset:length.`<br/> **Data di rilascio: 09/13/18** </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. length) </li> <li> **Heartbeats:**<br/> (l: risorse: length) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Lunghezza contenuto (variabile) </li> <li> **Dati contestuali:**<br/> (a. media. length) </li> <li> **Feed dati:**<br/> videolength </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. length </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Lunghezza video

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media. length </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> VOD: 128; Live: 86400; Lineare: 1800. </li> <li> **Descrizione:**<br/> Lunghezza/Fase di esecuzione delle clip - Questa è la lunghezza massima (o durata) del contenuto in uso (in secondi). It equals the last value of `l:asset:length` from events of type Main. If `l:asset:length` is not set, then the last value of `l:asset:duration` is used. In reporting, Video Length is the classification, and Content Length (variable) is the eVAR.  <br/> **Importante:** Questa proprietà viene utilizzata per calcolare diverse metriche, ad esempio metriche di tracciamento dell'avanzamento e Pubblico medio minuto. Se non è impostata, o non è maggiore di zero, queste metriche non sono disponibili. Per gli elementi multimediali live con durata sconosciuta, il valore predefinito è 86400. Pre Version 1.5.1, this was `l:asset:duration`; after 1.5.1, this is `l:asset:length.`<br/> **Data di rilascio: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. length) </li> <li> **Heartbeats:**<br/> (l: risorse: length) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Lunghezza video </li> <li> **Dati contestuali:**<br/> (a. media. length) </li> <li> **Feed dati:**<br/> weblassificationlength </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. length </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Tipo di contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [Streamtype](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media. contenttype </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> stringa limitata </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> " vod " </li> <li> **Descrizione:**<br/> Valori disponibili per **Tipo flusso**: <br/> _Audio:_ " song "," podcast "," audiobook "," radio " <br/> _Video:_ " Vod "," Live "," Linear "," UGC "," dvod " <br/> Clienti possono fornire valori personalizzati per questo parametro. This equals `s:stream:type.` If that is unset, this equals `missing_content_type.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. contenttype) </li> <li> **Heartbeats:**<br/> (s: stream: type) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Tipo di contenuto </li> <li> **Dati contestuali:**<br/> (a. contenttype) </li> <li> **Feed dati:**<br/> videocontenttype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID sessione multimediale

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> Ottenuto dal backend </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.8 </li> <li> **Valore di esempio:**<br/> 1482236761294786918253 </li> <li> **Descrizione:**<br/> Ciò identifica un'istanza di un flusso di contenuto univoca per una singola riproduzione.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. vsid) </li> <li> **Heartbeat:**<br/> (s: evento: sid) </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a. media. vsid) </li> <li> **Feed dati:**<br/> vsid </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. vsid) </li> </ul> |

### Nome lettore contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [Playername](./audio-video-parameters.md#config-media-object) </li> <li> **Chiave API:**<br/> media. playername </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> " Brightcove " </li> <li> **Descrizione:**<br/> Nome del lettore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Playername) </li> <li> **Heartbeats:**<br/> (s: sp: player_ name) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Nome lettore contenuto </li> <li> **Dati contestuali:**<br/> (a. media. playername) </li> <li> **Feed dati:**<br/> videoplayername </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. playername) </li> </ul> |

### Canale contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **Chiave API:**<br/> media. channel </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> " Sport " </li> <li> **Descrizione:**<br/> Distribution Station/Canali o in cui viene riprodotto il contenuto. Qualsiasi valore di stringa viene accettato qui.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. channel) </li> <li> **Heartbeats:**<br/> (s: sp: canale) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Canale contenuto </li> <li> **Dati contestuali:**<br/> (a. media. channel) </li> <li> **Feed dati:**<br/> videochannel </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. channel) </li> </ul> |

### Segmento contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> Sì </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> " 0-10 " </li> <li> **Descrizione:**<br/> Intervallo che descrive la parte del contenuto visualizzata (in minuti). Il segmento viene calcolato come min e max dei valori dell'indicatore di riproduzione durante una sessione di riproduzione.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Segmento contenuto </li> <li> **Dati contestuali:**<br/> (a. media. segment) </li> <li> **Feed dati:**<br/> videosegmento </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.segment) </li> </ul> |

### Nome contenuto (variabile)

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media. name </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.1 </li> <li> **Valore di esempio:**<br/> «The Big Bang Theory» </li> <li> **Descrizione:**<br/>Questo è il nome "intuitivo" (leggibile dall'uomo) del contenuto, pari all'ultimo valore di `s:asset:name.`<br/>In reporting, Nome video è la classificazione e Nome contenuto (variabile) è la evar. <br/> **Data di rilascio: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Friendlyname) </li> <li> **Heartbeats:**<br/> (s: risorse: name) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Nome contenuto (variabile) </li> <li> **Dati contestuali:**<br/> (a. media. friendlyname) </li> <li> **Feed dati:**<br/> videoname </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. friendlyname) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Nome video

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **Chiave API:**<br/> media. name </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.1 </li> <li> **Valore di esempio:**<br/> «The Big Bang Theory» </li> <li> **Descrizione:**<br/> Questo è il nome "intuitivo" (leggibile dall'uomo) del contenuto, pari all'ultimo valore di `s:asset:name.`<br/>In reporting, Nome video è la classificazione e Nome contenuto (variabile) è la evar. <br/> **Data di rilascio: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Friendlyname) </li> <li> **Heartbeats:**<br/> (s: risorse: name) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Nome video </li> <li> **Dati contestuali:**<br/> (a. media. friendlyname) </li> <li> **Feed dati:**<br/> weblassificationname </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. friendlyname) </li> </ul> |

### Percorso video

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> " 4586695 ABC " </li> <li> **Descrizione:**<br/> Consente di monitorare il percorso di un visualizzatore su un sito e/o un'app, per visualizzare il percorso che hanno acquisito per visualizzare un particolare video. Qualsiasi combinazione di numero intero e/o lettera.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. name) </li> <li> **Heartbeats:**<br/> (s: risorse: video_ id) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> prop </li> <li> **Nome rapporto:**<br/> Percorso video </li> <li> **Dati contestuali:**<br/> (a. media. name) </li> <li> **Feed dati:**<br/> videopath </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.name) </li> </ul> |

### Versione SDK

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [Appversion](./audio-video-parameters.md#config-media-object) </li> <li> **Chiave API:**<br/> media. sdkversion </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> " 2.62.0_ release " </li> <li> **Descrizione:**<br/> Versione SDK utilizzata dal lettore. Può avere un qualsiasi valore personalizzato che abbia senso per il lettore. <br/><br/>I clienti dovranno creare le proprie regole di elaborazione per rendere disponibile il valore per il reporting.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Sdkversion) </li> <li> **Heartbeats:**<br/> (s: sp: sdk) </li> </ul> | <ul> <li> **Disponibile:**<br/> Utilizzare la regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/> (a. media. sdkversion) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. sdkversion) </li> </ul> |

### Versione VHL

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> " js -2.0.1.88-c 8 c 0 b 1 " </li> <li> **Descrizione:**<br/> Versione Heartbeat SDK utilizzata per la sessione di tracciamento. <br/><br/>I clienti dovranno creare le proprie regole di elaborazione per rendere disponibile il valore per il reporting. <br/><br/>[Mediaheartbeat. version ();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media.<br/>Vhlversion) </li> <li> **Heartbeats:**<br/> (s: sp: hb_ version) </li> </ul> | <ul> <li> **Disponibile:**<br/> Utilizzare la regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a. media. vhlversion) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. vhlversion) </li> </ul> |

## Metadati audio e video standard {#section_pfc_hbm_n1b}

### Mostra le informazioni

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> SHOW </li> <li> **Chiave API:**<br/> media. show </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> " Modern Family "" Blacklist "" New Girl " </li> <li> **Descrizione:**<br/> Nome <br/>programma Nome serie/Nome serie è richiesto solo se la visualizzazione fa parte di una serie.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. show) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. show) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Mostra </li> <li> **Dati contestuali:**<br/> (a. media. show) </li> <li> **Feed dati:**<br/> videoshow </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. show) </li> </ul> |

### Formato flusso

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> STREAM_ FORMAT </li> <li> **Chiave API:**<br/> N/D </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> " Live " </li> <li> **Descrizione:**<br/> Formato del flusso (Live, VOD, Lineare).  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. format) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. format) </li> </ul> | <ul> <li> **Disponibile:**<br/> Utilizzare la regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a. media. format) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. format) </li> </ul> |

### Stagione

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> SEASON </li> <li> **Chiave API:**<br/> media. season </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> " 2 " </li> <li> **Descrizione:**<br/> Il numero di stagione a cui appartiene l'show. La serie stagione è necessaria solo se la visualizzazione fa parte di una serie.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. season) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. season) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Stagione </li> <li> **Dati contestuali:**<br/> (a. media. season) </li> <li> **Feed dati:**<br/> videoseason </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. season) </li> </ul> |

### Episodio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> EPISODIO </li> <li> **Chiave API:**<br/> media. episode </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> " 13 " </li> <li> **Descrizione:**<br/> Il numero dell'episodio.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. episode) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. episode) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Episodio </li> <li> **Dati contestuali:**<br/> (a. media. episode) </li> <li> **Feed dati:**<br/> videoepisodio </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. episode) </li> </ul> |

### ID risorsa

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> ASSET_ ID </li> <li> **Chiave API:**<br/> media. assetid </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> " 89745363 " </li> <li> **Descrizione:**<br/> Si tratta dell'identificatore univoco per il contenuto della risorsa multimediale, come l'identificatore dell'episodio serie TV, l'identificatore delle risorse del filmato o l'identificatore eventi live. In genere questi ID sono derivati da autorità di metadati quali EIDR, TMS/Gracenote o Rovi. Tali identificatori possono essere di altri sistemi proprietari o interni.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. asset) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. asset) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> ID risorsa </li> <li> **Dati contestuali:**<br/> (a. media. asset) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. asset) </li> </ul> |

### Genere

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> GENRE </li> <li> **Chiave API:**<br/> media. genre </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> «Drama», «Comedy» </li> <li> **Descrizione:**<br/> Tipo o raggruppamento del contenuto come definito da content producer. I valori devono essere delimitati da virgole nell'implementazione della variabile. Nel rapporto, la evar elenco suddivide ogni valore in un elemento di riga, con ogni elemento della riga che riceve spessore di metrica uguale.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. genre) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. genre) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar elenco </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Genere </li> <li> **Dati contestuali:**<br/> (a. media. genre) </li> <li> **Feed dati:**<br/> videogenre </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. genre) </li> </ul> |

### Data prima AIR

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> FIRST_ AIR_ DATE </li> <li> **Chiave API:**<br/> media. firstairdate </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> " 2016-01-25 " </li> <li> **Descrizione:**<br/> La data in cui il contenuto è passato per la prima volta sul televisore. Qualsiasi formato di data è accettabile, ma Adobe consiglia: AAAA-MM-DD </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. airdate) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. airdate) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Data prima AIR </li> <li> **Dati contestuali:**<br/> (a. media. airdate) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. airdate) </li> </ul> |

### Prima data digitale

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> FIRST_ DIGITAL_ DATE </li> <li> **Chiave API:**<br/> media. firstdigitaldate </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> " 2016-01-25 " </li> <li> **Descrizione:**<br/> La data in cui il contenuto è stato visualizzato per la prima volta su un qualsiasi canale digitale o piattaforma. Qualsiasi formato di data è accettabile, ma Adobe consiglia: AAAA-MM-DD </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. digitaldate) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. digitaldate) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Prima data digitale </li> <li> **Dati contestuali:**<br/> (a. media. digitaldate) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. digitaldate) </li> </ul> |

### Valutazione contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> VALUTAZIONE </li> <li> **Chiave API:**<br/> media. rating </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> TVY, TVG, TVPG, TVMA </li> <li> **Descrizione:**<br/> Valutazione come definito dalle linee guida per i genitori TV.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. rating) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. rating) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Valutazione contenuto </li> <li> **Dati contestuali:**<br/> (a. media. rating) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. rating) </li> </ul> |

### Originator

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> ORIGINATOR </li> <li> **Chiave API:**<br/> media. originator </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> " Warner Brothers "," Sony "," Disney " </li> <li> **Descrizione:**<br/> Creatore del contenuto.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. originator) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. originator) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Originator </li> <li> **Dati contestuali:**<br/> (a. media. originator) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. originator) </li> </ul> |

### Rete

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> NETWORK </li> <li> **Chiave API:**<br/> media. network </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> " Fox "," Bravo "," ESPN " </li> <li> **Descrizione:**<br/> Il nome di rete/canale.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. network) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. network) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Rete </li> <li> **Dati contestuali:**<br/> (a. media. network) </li> <li> **Feed dati:**<br/> videonetwork </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. network) </li> </ul> |

### Mostra tipo

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> SHOW_ TYPE </li> <li> **Chiave API:**<br/> media. showtype </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> " 0 " = Full episode; " 1 " = Preview/trailer; " 2 " = Clip; " 3 " = Altro. </li> <li> **Descrizione:**<br/> Tipo di contenuto, espresso sotto forma di numero intero compreso tra 0 e 3.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. type) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. type) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Mostra tipo </li> <li> **Dati contestuali:**<br/> (a. media. type) </li> <li> **Feed dati:**<br/> videoshowtype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. type) </li> </ul> |

### MVPD

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> MVPD </li> <li> **Chiave API:**<br/> media. pass. mvpd </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> " Comcast "," directv "," Dish " </li> <li> **Descrizione:**<br/> MVPD fornito tramite l'autenticazione Adobe.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. pass. mvpd) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. pass.<br/>mvpd) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> MVPD </li> <li> **Dati contestuali:**<br/> (a. media. pass. mvpd) </li> <li> **Feed dati:**<br/> videomvpd </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. pass. mvpd) </li> </ul> |

### Autorizzato

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> AUTHORIZED </li> <li> **Chiave API:**<br/> media. pass. auth </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> " TRUE " </li> <li> **Descrizione:**<br/> L'utente è stato autorizzato tramite l'autenticazione Adobe. <br/>**Importante:** Questo può essere true solo se impostato. Se non viene impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. pass. auth) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. pass.<br/>auth) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Autorizzato </li> <li> **Dati contestuali:**<br/> (a. media. pass. auth) </li> <li> **Feed dati:**<br/> videoauthorized </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. pass. auth) </li> </ul> |

### Part Part

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> DAY_ PART </li> <li> **Chiave API:**<br/> media. daypart </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> </li> <li> **Descrizione:**<br/> Proprietà che definisce l'ora del giorno in cui è stato trasmesso o riprodotto il contenuto. Questo potrebbe avere un qualsiasi valore impostato dai clienti.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. daypart) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. daypart) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Part Part </li> <li> **Dati contestuali:**<br/> (a. media. daypart) </li> <li> **Feed dati:**<br/> videodaypart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. daypart) </li> </ul> |

### Tipo feed multimediale

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> FEED </li> <li> **Chiave API:**<br/> media. feed </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 </li> <li> **Valore di esempio:**<br/> " East-HD "," West-HD "," East-SD " </li> <li> **Descrizione:**<br/> Tipo di feed. <br/> **Data di rilascio: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. feed) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. feed) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> Tipo feed multimediale </li> <li> **Dati contestuali:**<br/> (a. media. feed) </li> <li> **Feed dati:**<br/> videofeedtype </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. feed) </li> </ul> |

### Artista

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media. artist </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> «The Beatles» </li> <li> **Descrizione:**<br/> Nome dell'artista. <br/> **Data di rilascio: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. artist) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. artist) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/> (a. media. artist) </li> <li> **Feed dati:**<br/> videoaudioartist </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. artist) </li> </ul> |

### Album

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media. album </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> " Rivoluzione " </li> <li> **Descrizione:**<br/> Nome dell'album. <br/> **Data di rilascio: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. album) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. album) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/> (a. media. album) </li> <li> **Feed dati:**<br/> videoaudioalbum </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. album) </li> </ul> |

### Etichetta

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media. label </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> " Rivoluzione " </li> <li> **Descrizione:**<br/> Nome dell'etichetta del record. <br/> **Data di rilascio: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. label) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. label) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/> (a. media. label) </li> <li> **Feed dati:**<br/> videoaudiolabel </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. label) </li> </ul> |

### Autore

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media. author </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> " John Kennedy Toole " </li> <li> **Descrizione:**<br/> Nome dell'autore (di un libro). <br/> **Data di rilascio: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. author) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. author) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/> (a. media. author) </li> <li> **Feed dati:**<br/> videoaudioauthor </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. author) </li> </ul> |

### Stazione

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media. station </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> " NPR " </li> <li> **Descrizione:**<br/> Nome/ID della stazione radio. <br/> **Data di rilascio: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. station) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. station) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/> (a. media. station) </li> <li> **Feed dati:**<br/> videoaudiostation </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. station) </li> </ul> |

### Editore

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media. publisher </li> <li> **Richiesto:**<br/> No </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Inizio file multimediali, Chiudi file multimediali </li> <li> **Min. SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](/help/media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> " Random Bauhaus " </li> <li> **Descrizione:**<br/> Nome dell'editore del contenuto audio. <br/> **Data di rilascio: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. publisher) </li> <li> **Heartbeats:**<br/> (s: meta:<br/>a. media. publisher) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Evar </li> <li> **Scadenza:**<br/> Su hit </li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/> (a. media. publisher) </li> <li> **Feed dati:**<br/> videoaudiopublisher </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. publisher) </li> </ul> |

## Audio and Video Metrics {#section_3D5F9C555274428AA6030D07596177E9}

### Inizio file multimediali

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico</li> <li> **Chiave API:**<br/> N/D</li> <li> **Tipo:**<br/> stringa</li> <li> **Inviato con:**<br/> Inizio file multimediali</li> <li> **Min. SDK Version:** Any</li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Carica evento per il supporto. (This occurs when the viewer clicks the _Play_ button). Questo dato viene conteggiato anche in presenza di annunci pre-roll, buffering, errori e così via. <br/>**Importante:** Questo può essere true solo se impostato. If it is not set, no value is returned.  <br/> **Data di rilascio: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a. media. view) </li> <li> **Heartbeats:**<br/> (s: evento:<br/>type = start) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Inizio file multimediali </li> <li> **Dati contestuali:**<br/> (a. media. view) </li> <li> **Feed dati:**<br/> videostart </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.view) </li> </ul> |

### Inizio contenuti

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Viene consumato il primo fotogramma di supporto. If the user drops during ad, buffering, etc., then there would be no "Content Start" event.  <br/> **Importante:** Questo può essere true solo se impostato. Se non viene impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Inizio contenuto </li> <li> **Dati contestuali:**<br/> (a. media. play) </li> <li> **Feed dati:**<br/> videoplay </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. play) </li> </ul> |

### Content Complete {#content-complete}

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Flusso visualizzato al completamento. Ciò significa che l'utente ha visualizzato o ignorato l'intero flusso, potevano essere ignorati. Ciò significa che l'utente ha raggiunto la fine del flusso, 100%. <br/>Vedi anche Fine [sessione](quality-parameters.md#session-end)<br/> **Importante:** Questo può essere true solo se impostato. Se non viene impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> (s: evento:<br/>type = complete) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Completamento dei contenuti </li> <li> **Dati contestuali:**<br/> (a. media. complete) </li> <li> **Feed dati:**<br/> videocomplete </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. complete) </li> </ul> |

### Tempo contenuto trascorso

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> 105 </li> <li> **Descrizione:**<br/> Somma la durata dell'evento (in secondi) per tutti gli eventi di tipo PLAY sul contenuto principale. Il valore verrà visualizzato nel formato temporale (HH: MM: SS) in Analysis Workspace e Reporting e analisi. In Data Feeds, Data Warehouse, and Reporting APIs the values will be displayed in seconds.  <br/> **Data di rilascio: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Tempo contenuto trascorso </li> <li> **Dati contestuali:**<br/> (a. media. timeplayed) </li> <li> **Feed dati:**<br/> videotime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.timePlayed) </li> </ul> |

### Tempo medio trascorso

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> 120 </li> <li> **Descrizione:**<br/> Somma la durata dell'evento (in secondi) per tutti gli eventi di tipo PLAY, sia main che ad. Il valore verrà visualizzato nel formato temporale (HH: MM: SS) in Analysis Workspace e Reporting e analisi. In Data Feeds, Data Warehouse, and Reporting APIs the values will be displayed in seconds.  <br/> **Data di rilascio: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Tempo medio trascorso </li> <li> **Dati contestuali:**<br/> (a. media. totaltimeplay) </li> <li> **Feed dati:**<br/> videototaltime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. totaltimeplay) </li> </ul> |

### Tempo univoco

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> 94 </li> <li> **Descrizione:**<br/> Il valore in secondi dei singoli segmenti di contenuto riprodotti durante una sessione. Esclude il tempo riprodotto negli scenari di ricerca in cui un visualizzatore guarda lo stesso segmento del contenuto più volte. Il valore verrà visualizzato nel formato temporale (HH: MM: SS) in Analysis Workspace e Reporting e analisi. In Data Feeds, Data Warehouse, and Reporting APIs the values will be displayed in seconds.  <br/> **Data di rilascio: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a. media. uniquetimeplay) </li> <li> **Feed dati:**<br/> videouniquetimeplay </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. uniquetimeplay) </li> </ul> |

### Marcatore progresso dieci %

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> La linea di scansione passa il marcatore 10% di contenuto in base alla lunghezza. Il marcatore viene conteggiato solo una volta, anche se si trova indietro. If seeking forward, markers that are skipped are not counted.  <br/> **Importante:** Questo può essere true solo se impostato. Se non viene impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Marcatore progresso 10% </li> <li> **Dati contestuali:**<br/> (a. media. progress 10) </li> <li> **Feed dati:**<br/> videoprogress 10 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. progress 10) </li> </ul> |

### Marcatore progresso di venticinque %

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> La linea di scansione passa il marcatore 25% del contenuto in base alla lunghezza del contenuto. Il marcatore è conteggiato solo una volta, anche se si trova indietro. If seeking forward, markers that are skipped are not counted.  <br/> **Importante:** Questo può essere true solo se impostato. Se non viene impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Marcatore progresso 25% </li> <li> **Dati contestuali:**<br/> (a. media. progress 25) </li> <li> **Feed dati:**<br/> videoprogress 25 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. progress 25) </li> </ul> |

### Marcatore progresso cinquanta %

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> La linea di scansione passa il marcatore 50% del contenuto in base alla lunghezza del contenuto. Il marcatore è conteggiato solo una volta, anche se si trova indietro. If seeking forward, markers that are skipped are not counted.  <br/> **Importante:** Questo può essere true solo se impostato. Se non viene impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Marcatore progresso 50% </li> <li> **Dati contestuali:**<br/> (a. media. progress 50) </li> <li> **Feed dati:**<br/> videoprogress 50 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. progress 50) </li> </ul> |

### Marcatore progresso %

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> **N/D** </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> La linea di scansione passa il marcatore 75% del contenuto in base alla lunghezza del contenuto. Il marcatore è conteggiato solo una volta, anche se si trova indietro. If seeking forward, markers that are skipped are not counted.  <br/> **Importante:** Questo può essere true solo se impostato. Se non viene impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Marcatore progresso 75% </li> <li> **Dati contestuali:**<br/> (a. media. progress 75) </li> <li> **Feed dati:**<br/> videoprogress 75 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. progress 75) </li> </ul> |

### Marcatore progresso novanta %

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> La linea di scansione passa il marcatore 95% del contenuto in base alla lunghezza del contenuto. Il marcatore è conteggiato solo una volta, anche se si trova indietro. If seeking forward, markers that are skipped are not counted.  <br/> **Importante:** Questo può essere true solo se impostato. Se non viene impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Marcatore progresso 95% </li> <li> **Dati contestuali:**<br/> (a. media. progress 95) </li> <li> **Feed dati:**<br/> videoprogress 95 </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. progress 95) </li> </ul> |

### Pubblico medio per minuto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> Maggiore o uguale a 1 </li> <li> **Descrizione:**<br/> La metrica Audience minuti media viene calcolata come Tempo totale contenuto trascorso, per un elemento multimediale specifico, diviso per la lunghezza per tutte le sessioni di riproduzione: <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Pubblico medio minuto </li> <li> **Dati contestuali:**<br/> (a. media. averageminuteaudience) </li> <li> **Feed dati:**<br/> videoaverageminutututeaudience </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. averageminuteaudience) </li> </ul> |

### Flussi stimati

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> 1 - Per una riproduzione di 19 minuti; <br/>2 - Per una riproduzione di 31 minuti; <br/>3 - Per una riproduzione di 78 minuti. </li> <li> **Descrizione:**<br/> Numero stimato di flussi audio o video per ciascun singolo contenuto. Questo valore viene aumentato per ogni 30 minuti di tempo di riproduzione (contenuto + annunci). I clienti devono creare le proprie regole di elaborazione per avere il valore disponibile per il reporting. <br/><br/>Un flusso viene conteggiato ogni 30 minuti, in base al `ms_s` Tempo totale (o totaltimeplayed = Video Totale), simile a: <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Utilizzare la regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a. media. estimatedstreams) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. estimatedstreams) </li> </ul> |

### Flussi interessati in pausa

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** 1.5.6 </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Questo valore è vero o falso. It is true if one or more pauses occurred during playback of a single media item.  <br/> **Importante:** Questo può essere true solo se impostato. Se non viene impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> (s: evento:<br/>type = pause) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Flusso interessati in pausa </li> <li> **Dati contestuali:**<br/> (a. media. pause) </li> <li> **Feed dati:**<br/> videopause </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. pause) </li> </ul> |

### Sospendi eventi

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** 1.5.6 </li> <li> **Valore di esempio:**<br/> 2 </li> <li> **Descrizione:**<br/> Questa metrica viene calcolata come un numero di periodi di pausa che si sono verificati durante una sessione di riproduzione.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> (s: evento:<br/>type = pause) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Sospendi eventi </li> <li> **Dati contestuali:**<br/> (a. media. pausecount) </li> <li> **Feed dati:**<br/> videopausecount </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. pausecount) </li> </ul> |

### Durata totale pausa

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** 1.5.6 </li> <li> **Valore di esempio:**<br/> 190 </li> <li> **Descrizione:**<br/> Somma la durata (in secondi) di tutti gli eventi di tipo PAUSE. Il valore verrà visualizzato nel formato temporale (HH: MM: SS) in Analysis Workspace e Reporting e analisi. In Data Feeds, Data Warehouse, and Reporting APIs the values will be displayed in seconds. <br/> **Data di rilascio: 09/13/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Durata totale pausa </li> <li> **Dati contestuali:**<br/> (a. media. pausetime) </li> <li> **Feed dati:**<br/> videopausetime </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. pausetime) </li> </ul> |

### Ripresa contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> **media. resume** </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** 1.5.6 </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Viene conteggiato un riprendi per ogni riproduzione che riprende dopo oltre 30 minuti di buffer, pausa o stall punto OPPURE se questo valore è impostato dal lettore in videoinfo trackplay. <br/> **Importante:** Questo può essere true solo se impostato. Se non viene impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> (s: evento:<br/>type = resume) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Ripresa contenuto </li> <li> **Dati contestuali:**<br/> (a. media. resume) </li> <li> **Feed dati:**<br/> videoresume </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a. media. resume) </li> </ul> |

### Visualizzazioni dei segmenti di contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Set automatico </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> stringa </li> <li> **Inviato con:**<br/> Chiudi supporto </li> <li> **Min. SDK Version:** Any </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Numero di visualizzazioni del contenuto principale. A Content Segment View is counted when there is at least one frame viewed.  <br/> **Importante:** Questo può essere true solo se impostato. Se non viene impostato, non viene restituito alcun valore. </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeats:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> evento </li> <li> **Nome rapporto:**<br/> Visualizzazioni dei segmenti di contenuto </li> <li> **Dati contestuali:**<br/> (a. media. segmentview) </li> <li> **Feed dati:**<br/> videosegmentazioni </li> <li> **Audience Manager:**<br/> (c_ contextdata.<br/>a.media.segmentView) </li> </ul> |

## Related APIs {#section_Related_APIs}

### createMediaObject APIs {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig APIs {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)

