---
seo-title: Parametri audio e video
title: Parametri audio e video
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
translation-type: tm+mt
source-git-commit: 89870fcf20bdfa75a178ffc2124498b94cabe4a7

---


# Parametri audio e video{#audio-and-video-parameters}

>[!IMPORTANT]
>
>Il 7 febbraio 2019, Adobe Analytics per Video e Audio ha rilasciato una modifica al nome della metrica. <i>Media Initiates</i> verrà ora denominato <i>Media Starts</i>. Questa modifica è stata apportata per riflettere gli standard di settore nelle metriche e nei report e per rendere la metrica facilmente identificabile nei report.

>[!NOTE]
>
>A partire dal 13 settembre 2018 è stata apportata una modifica alle etichette per alcune dimensioni, metriche e rapporti, per consentire il tracciamento tra contenuti delle analisi video e audio. Le etichette modificate includono: Il *video viene avviato* alle iniziazioni *del file multimediale*, la lunghezza *del* video alla lunghezza *del* contenuto e il nome *del* ** video al nome del contenuto . I rapporti video in Reporting e analisi sono stati tutti aggiornati per utilizzare il nome "File multimediali" anziché "Video". Le modifiche alle etichette non hanno modificato la raccolta dati o i dati storici. Prendete nota di queste modifiche nel caso in cui le stiate utilizzando in Generatore di report o in qualsiasi altra raccolta di dati automatizzata esterna che potrebbe essere influenzata da questa modifica.

Questo argomento presenta un elenco di dati di contenuto audio e video, inclusi i valori dei dati contestuali, raccolti da Adobe tramite variabili della soluzione.

Descrizione dati tabella:

* **** Implementazione: Informazioni su valori e requisiti di implementazione
   * *Chiave* - Variabile, impostata manualmente nell’app o automaticamente dall’SDK di Adobe Media.
   * *Obbligatorio* - Indica se il parametro è richiesto per il tracciamento audio e video di base.
   * *Tipo* - Specifica il tipo di variabile da impostare, stringa o numero.
   * *Inviato con* - Indica quando i dati vengono inviati: *Media Start* è la chiamata di analisi inviata all’avvio del supporto, *Ad Start* è la chiamata di analisi inviata all’inizio e all’inizio dell’annuncio, e così via; le chiamate *Close* sono le chiamate di analisi compilate inviate direttamente dal server Heartbeat al server di analisi alla fine della sessione multimediale, o la fine dell'annuncio, del capitolo, ecc. Le chiamate di chiusura non sono disponibili nelle chiamate dei pacchetti di rete.
   * *Min. Versione* SDK - Indica la versione SDK a cui sarà necessario accedere per il parametro.
   * *Valore* di esempio - Fornisce un esempio di utilizzo comune delle variabili.
* **** Parametri di rete: Visualizza i valori passati ai server Adobe Analytics o Heartbeat. Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate dagli SDK di Adobe Media.
* **** Reporting: Informazioni su come visualizzare e analizzare i dati audio e video.
   * *Disponibile* - Indica se i dati sono disponibili nel reporting per impostazione predefinita (*Sì*) o richiedono una configurazione personalizzata (*Personalizzato*)
   * *Variabile* riservata - Indica se i dati vengono acquisiti come evento, eVar, prop o classificazione in una variabile riservata.
   * *Scadenza* - Indica se i dati scadono dopo ogni hit o dopo ogni visita.
   * *Nome* report - Nome del report Adobe Analytics per la variabile
   * *Dati* contestuali - Nome dei dati contestuali di Adobe Analytics passati al server di reporting e utilizzati nelle regole di elaborazione.
   * *Feed* dati - Nome colonna per la variabile trovata nei feed di dati Clickstream o Live Stream
   * *Audience Manager* - Nome caratteristica trovato in Adobe Audience Manager

>[!IMPORTANT]
>
>Non modificare i nomi delle classificazioni per le variabili elencate di seguito che sono descritte in Reporting/Riservato Variabile come "classificazione".\
>Le classificazioni dei supporti vengono definite quando una suite di rapporti è abilitata per il tracciamento dei supporti. Di tanto in tanto, Adobe aggiunge nuove proprietà e, in questo caso, i clienti devono riabilitare le suite di rapporti per poter accedere alle nuove proprietà del supporto. Durante il processo di aggiornamento, Adobe determina se le classificazioni sono abilitate controllando i nomi delle variabili. Se manca qualcuno di essi, Adobe aggiunge di nuovo quelli mancanti.

## Dati audio e video di base {#section_y55_y1m_n1b}

### Tipo di flusso {#stream-type}

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> ****<br/> Chiave API: media.streamType </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 2.2 <br/><br/>Disponibile in Panoramica [dell'API di](/help/media-collection-api/mc-api-overview.md) Media Collection o [Download di SDK - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> ****<br/> Valore di esempio: "video" </li> <li> ****<br/> Descrizione: Identifica il tipo di flusso. I valori validi sono "audio", "video" e ".  <br/><br/>[Segmenti](/help/metrics-and-metadata/segments.md)di reporting: Tipo di flusso <br/><br/>multimediale: All - <br/>Segment all media stream data; Regola: Il contenuto (ID) esiste come tipo di flusso <br/><br/>multimediale: Audio - <br/>Segmenta tutti i dati del flusso audio; Regola: Contenuto (ID) esiste e tipo flusso multimediale = tipo flusso <br/><br/>multimediale audio: "Video" - <br/>Segmenta tutti i dati del flusso video; Regola: Il contenuto (ID) esiste e il tipo di flusso multimediale != audio <br/><br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.streamType) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.streamType) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: In visita </li> <li> ****<br/> Nome rapporto: Contenuto </li> <li> ****<br/> Dati contestuali: (a.media.streamType) </li> <li> ****<br/> Feed dati: videostreamtype </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> ****<br/> Chiave API: media.id </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: "4586695ABC" </li> <li>****<br/> Descrizione: ID contenuto del contenuto, che può essere utilizzato per collegarsi ad altri ID settore/CMS, pari all'ultimo valore di `s:asset:video_id.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.name) </li> <li> ****<br/> Heartbeat: (s:asset:video_id) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: In visita </li> <li> ****<br/> Nome rapporto: Contenuto </li> <li> ****<br/> Dati contestuali: (a.media.name) </li> <li> ****<br/> Feed dati: video </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

###  Lunghezza contenuto (variabile)

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> ****<br/> Chiave API: media.length </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: VOD: 128; Live: 86400; Lineare: 1800. </li><li> ****<br/> Descrizione: Lunghezza clip/Runtime: lunghezza (o durata) massima del contenuto utilizzato (in secondi). È uguale all'ultimo valore di `l:asset:length` da eventi di tipo Main. <br/>Se non `l:asset:length` è impostato, viene utilizzato l'ultimo valore di `l:asset:duration` . <br/>Nel reporting, Lunghezza video è la classificazione e Lunghezza contenuto (variabile) è l’eVAR.  <br/> **** Importante: Questa proprietà viene utilizzata per calcolare diverse metriche, come le metriche di tracciamento dell'avanzamento e il pubblico medio in minuti. Se non è impostato o non è maggiore di zero, queste metriche non sono disponibili.  Per i contenuti multimediali live di durata sconosciuta, il valore predefinito è 86400. <br/>Prima della versione 1.5.1, si trattava `l:asset:duration`; dopo il 1.5.1, questo è `l:asset:length.`<br/> **Data di rilascio: 13/09/18** </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.length) </li> <li> ****<br/> Heartbeat: (l:asset:length) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Lunghezza contenuto (variabile) </li> <li> ****<br/> Dati contestuali: (a.media.length) </li> <li> ****<br/> Feed dati: lunghezza video </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Lunghezza video

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> ****<br/> Chiave API: media.length </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: VOD: 128; Live: 86400; Lineare: 1800. </li> <li> ****<br/> Descrizione: Lunghezza clip/Runtime: lunghezza (o durata) massima del contenuto utilizzato (in secondi). È uguale all'ultimo valore di `l:asset:length` da eventi di tipo Main. Se non `l:asset:length` è impostato, viene utilizzato l'ultimo valore di `l:asset:duration` . Nel reporting, Lunghezza video è la classificazione e Lunghezza contenuto (variabile) è l’eVAR.  <br/> **** Importante: Questa proprietà viene utilizzata per calcolare diverse metriche, come le metriche di tracciamento dell'avanzamento e il pubblico medio in minuti. Se non è impostato o non è maggiore di zero, queste metriche non sono disponibili.  Per i contenuti multimediali live di durata sconosciuta, il valore predefinito è 86400. Prima della versione 1.5.1, si trattava `l:asset:duration`; dopo la versione 1.5.1 `l:asset:length.`<br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.length) </li> <li> ****<br/> Heartbeat: (l:asset:length) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: Classificazione </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto: Lunghezza video </li> <li> ****<br/> Dati contestuali: (a.media.length) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Tipo di contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> ****<br/> Chiave API: media.contentType </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: stringa limitata </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: "vod" </li> <li> ****<br/> Descrizione: Valori disponibili per tipo **di** flusso: <br/> __ Audio: "canzone", "podcast", "audiobook", "radio" <br/> __ Video: "VoD", "Live", "Linear", "UGC", "DVoD" <br/> I clienti possono fornire valori personalizzati per questo parametro. È uguale a `s:stream:type.` Se non viene impostato, è uguale a `missing_content_type.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.contentType) </li> <li> ****<br/> Heartbeat: (s:stream:type) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Tipo di contenuto </li> <li> ****<br/> Dati contestuali: (a.contentType) </li> <li> ****<br/> Feed dati: videocontenttype </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID sessione multimediale

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: Ottenuto dal back-end </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.8 </li> <li> ****<br/> Valore di esempio: 1482236761294786918253 </li> <li> ****<br/> Descrizione: Questo identifica un'istanza di un flusso di contenuto univoco per una singola riproduzione.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.vsid) </li> <li> ****<br/> Heartbeat: (s:event:sid) </li> </ul> | <ul> <li> ****<br/> Disponibile: Usa regola di elaborazione </li> <li> ****<br/> Variabile riservata: N/D </li> <li> ****<br/> Nome rapporto: Personalizzato </li> <li> ****<br/> Dati contestuali: (a.media.vsid) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.vsid) </li> </ul> |

###  Nome lettore contenuti

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> ****<br/> Chiave API: media.playerName </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: "Brightcove" </li> <li> ****<br/> Descrizione: Nome del giocatore.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>playerName) </li> <li> ****<br/> Heartbeat: (s:sp:player_name) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto: Nome lettore contenuti </li> <li> ****<br/> Dati contestuali: (a.media.playerName) </li> <li> ****<br/> Feed dati: videoplayername </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.playerName) </li> </ul> |

### Canale contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> ****<br/> Chiave API: media.channel </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: "Sport" </li> <li> ****<br/> Descrizione: Stazione di distribuzione/Canali o dove viene riprodotto il contenuto. Qualsiasi valore di stringa è accettato qui.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.channel) </li> <li> ****<br/> Heartbeat: (s:sp:channel) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Canale contenuto </li> <li> ****<br/> Dati contestuali: (a.media.channel) </li> <li> ****<br/> Feed dati: videocanale </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.channel) </li> </ul> |

### Segmento di contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Obbligatorio: Yes </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: "0-10" </li> <li> ****<br/> Descrizione: Intervallo che descrive la parte del contenuto visualizzata (in minuti). Il segmento viene calcolato come minimo e massimo dei valori dell'indicatore di riproduzione durante una sessione di riproduzione.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: N/D </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Segmento di contenuto </li> <li> ****<br/> Dati contestuali: (a.media.segment) </li> <li> ****<br/> Feed dati: videosegmento </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.segment) </li> </ul> |

###  Nome contenuto (variabile)

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> ****<br/> Chiave API: media.name </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.1 </li> <li> ****<br/> Valore di esempio: "La Teoria del Big Bang" </li> <li> **Descrizione:**<br/>questo è il nome "descrittivo" (leggibile dall'uomo) del contenuto, uguale all'ultimo valore di `s:asset:name.`<br/>Nel rapporto, Nome video è la classificazione, e Nome contenuto (variabile) è l'eVAR. <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>friendlyName) </li> <li> ****<br/> Heartbeat: (s:asset:name) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Nome contenuto (variabile) </li> <li> ****<br/> Dati contestuali: (a.media.friendlyName) </li> <li> ****<br/> Feed dati: videoname </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### Nome video

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> ****<br/> Chiave API: media.name </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.1 </li> <li> ****<br/> Valore di esempio: "La Teoria del Big Bang" </li> <li> ****<br/> Descrizione: Si tratta del nome "descrittivo" (leggibile dall’uomo) del contenuto, uguale all’ultimo valore di `s:asset:name.` <br/>Nel reporting, Nome video è la classificazione, e Nome contenuto (variabile) è l’eVAR.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>friendlyName) </li> <li> ****<br/> Heartbeat: (s:asset:name) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: Classificazione </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto: Nome video </li> <li> ****<br/> Dati contestuali: (a.media.friendlyName) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

### Percorso video

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Media Start </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: "4586695ABC" </li> <li> ****<br/> Descrizione: Consente di tenere traccia del percorso di un visualizzatore in un sito e/o in un’app, per visualizzare il percorso seguito per visualizzare un particolare video. Qualsiasi combinazione di numeri interi e/o lettere.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.name) </li> <li> ****<br/> Heartbeat: (s:asset:video_id) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: prop </li> <li> ****<br/> Nome rapporto: Percorso video </li> <li> ****<br/> Dati contestuali: (a.media.name) </li> <li> ****<br/> Feed dati: videopath </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.name) </li> </ul> |

### Versione SDK

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> ****<br/> Chiave API: media.sdkVersion </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore di esempio: "2.62.0_release" </li> <li> ****<br/> Descrizione: Versione SDK utilizzata dal lettore. Questo potrebbe avere qualsiasi valore personalizzato che abbia senso per il lettore. <br/><br/>I clienti dovranno creare le proprie regole di elaborazione per avere il valore disponibile per il reporting.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>sdkVersion) </li> <li> ****<br/> Heartbeat: (s:sp:sdk) </li> </ul> | <ul> <li> ****<br/> Disponibile: Usa regola di elaborazione personalizzata </li> <li> ****<br/> Variabile riservata: N/D </li> <li> **Nome rapporto:**<br/> </li> <li> ****<br/> Dati contestuali: (a.media.sdkVersion) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### Versione VHL

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore di esempio: "js-2.0.1.88-c8c0b1" </li> <li> ****<br/> Descrizione: Versione Media SDK utilizzata per la sessione di tracciamento. <br/><br/>I clienti dovranno creare le proprie regole di elaborazione per avere il valore disponibile per il reporting.  <br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>vhlVersion) </li> <li> ****<br/> Heartbeat: (s:sp:hb_version) </li> </ul> | <ul> <li> ****<br/> Disponibile: Usa regola di elaborazione personalizzata </li> <li> ****<br/> Variabile riservata: N/D </li> <li> ****<br/> Nome rapporto: Personalizzato </li> <li> ****<br/> Dati contestuali: (a.media.vhlVersion) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## Metadati audio e video standard {#section_pfc_hbm_n1b}

### Mostra le informazioni

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: MOSTRA </li> <li> ****<br/> Chiave API: media.show </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore di esempio: "Famiglia moderna" "Blacklist" "nuova ragazza" </li> <li> ****<br/> Descrizione: Nome <br/>programma/Serie Il nome del programma è richiesto solo se lo spettacolo fa parte di una serie.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.show) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.show) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Mostra </li> <li> ****<br/> Dati contestuali: (a.media.show) </li> <li> ****<br/> Feed dati: videoshow </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.show) </li> </ul> |

### Formato flusso

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: STREAM_FORMAT </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore di esempio: "Live" </li> <li> ****<br/> Descrizione: Formato del flusso (Live, VOD, Linear).  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.format) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.format) </li> </ul> | <ul> <li> ****<br/> Disponibile: Usa regola di elaborazione personalizzata </li> <li> ****<br/> Variabile riservata: N/D </li> <li> ****<br/> Nome rapporto: Personalizzato </li> <li> ****<br/> Dati contestuali: (a.media.format) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.format) </li> </ul> |

### Stagione

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: STAGIONE </li> <li> ****<br/> Chiave API: media.season </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore di esempio: "2" </li> <li> ****<br/> Descrizione: Il numero di stagione a cui appartiene lo spettacolo.  Stagione Serie è richiesto solo se lo show fa parte di una serie.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.stagione) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.stagione) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Stagione </li> <li> ****<br/> Dati contestuali: (a.media.stagione) </li> <li> ****<br/> Feed dati: videoconferenza </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.stagione) </li> </ul> |

### Episodio

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: EPISODE </li> <li> ****<br/> Chiave API: media.episode </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore di esempio: "13" </li> <li> ****<br/> Descrizione: Numero dell'episodio.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.episode) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.episode) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Episodio </li> <li> ****<br/> Dati contestuali: (a.media.episode) </li> <li> ****<br/> Feed dati: videoepisodio </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.episode) </li> </ul> |

###  ID risorsa

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: ASSET_ID </li> <li> ****<br/> Chiave API: media.assetId </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore di esempio: "89745363" </li> <li> ****<br/> Descrizione: Questo è l’identificatore univoco per il contenuto della risorsa multimediale, ad esempio l’identificatore episodio della serie TV, l’identificatore della risorsa filmato o l’identificatore evento live. In genere questi ID sono derivati da autorità di metadati quali EIDR, TMS/Gracenote o Rovi. Questi identificatori possono provenire anche da altri sistemi proprietari o interni.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.asset) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.asset) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: Classificazione </li> <li> ****<br/> Nome rapporto: ID risorsa </li> <li> ****<br/> Dati contestuali: (a.media.asset) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.asset) </li> </ul> |

### Genere

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: GENERE </li> <li> ****<br/> Chiave API: media.genre </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore di esempio: "Drama", "Comedy" </li> <li> ****<br/> Descrizione: Tipo o raggruppamento di contenuti come definito dal produttore di contenuti. I valori devono essere delimitati da virgole nell’implementazione della variabile. Nel reporting, l'eVar elenco dividerà ogni valore in un elemento riga, con ogni elemento riga che riceve lo stesso peso delle metriche.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.genre) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.genre) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: Elenco eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Genere </li> <li> ****<br/> Dati contestuali: (a.media.genre) </li> <li> ****<br/> Feed dati: videogenere </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.genre) </li> </ul> |

### Data primo Air

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: FIRST_AIR_DATE </li> <li> ****<br/> Chiave API: media.firstAirDate </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Media Start </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore di esempio: "2016-01-25" </li> <li> ****<br/> Descrizione: La data in cui il contenuto è andato in onda per la prima volta in televisione. Qualsiasi formato di data è accettabile, ma Adobe consiglia: AAAA-MM-GG </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.airDate) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.airDate) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: Classificazione </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Data primo Air </li> <li> ****<br/> Dati contestuali: (a.media.airDate) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.airDate) </li> </ul> |

### Prima data digitale

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: FIRST_DIGITAL_DATE </li> <li> ****<br/> Chiave API: media.firstDigitalDate </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore di esempio: "2016-01-25" </li> <li> ****<br/> Descrizione: Data in cui il contenuto è stato trasmesso per la prima volta su qualsiasi canale o piattaforma digitale. Qualsiasi formato di data è accettabile, ma Adobe consiglia: AAAA-MM-GG </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.digitalDate) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.digitalDate) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: Classificazione </li> <li> ****<br/> Nome rapporto:Prima data digitale </li> <li> ****<br/> Dati contestuali: (a.media.digitalDate) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.digitalDate) </li> </ul> |

###  Valutazione contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: VALUTAZIONE </li> <li> ****<br/> Chiave API: media.rating </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore di esempio: TVG, TVG, TVPG, TVMA </li> <li> ****<br/> Descrizione: Classificazione come definita dalle linee guida TV sui genitori.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.rating) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.rating) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: Classificazione </li> <li> ****<br/> Nome rapporto: Valutazione contenuto </li> <li> ****<br/> Dati contestuali: (a.media.rating) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.rating) </li> </ul> |

### Creatore

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: ORIGINATORE </li> <li> ****<br/> Chiave API: media.originator </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore di esempio: "Warner Brothers", "Sony", "Disney" </li> <li> ****<br/> Descrizione: Creatore del contenuto.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.originator) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.originator) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: Classificazione </li> <li> ****<br/> Nome rapporto:Creatore </li> <li> ****<br/> Dati contestuali: (a.media.originator) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.originator) </li> </ul> |

### Rete

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: RETE </li> <li> ****<br/> Chiave API: media.network </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore di esempio: "Fox", "Bravo", "ESPN" </li> <li> ****<br/> Descrizione: Nome della rete/del canale.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.network) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.network) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Rete </li> <li> ****<br/> Dati contestuali: (a.media.network) </li> <li> ****<br/> Feed dati: videonetwork </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.network) </li> </ul> |

### Mostra tipo

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: SHOW_TYPE </li> <li> ****<br/> Chiave API: media.showType </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore di esempio: "0" = episodio completo; "1" = Anteprima/trailer; "2" = Clip; "3" = Altro. </li> <li> ****<br/> Descrizione: Tipo di contenuto, espresso come numero intero compreso tra 0 e 3.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.type) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.type) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Mostra tipo </li> <li> ****<br/> Dati contestuali: (a.media.type) </li> <li> ****<br/> Feed dati: videoshowtype </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK:MVPD </li> <li> ****<br/> Chiave API: media.pass.mvpd </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore di esempio: "Comcast", "DirectTV", "Dish" </li> <li> ****<br/> Descrizione: MVPD fornito tramite autenticazione Adobe.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.pass.mvpd) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.pass.<br/>mvpd) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:MVPD </li> <li> ****<br/> Dati contestuali: (a.media.pass.mvpd) </li> <li> ****<br/> Feed dati: videomvpd </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### Autorizzato

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: AUTORIZZATO </li> <li> ****<br/> Chiave API: media.pass.auth </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore di esempio: "TRUE" </li> <li> ****<br/> Descrizione: L'utente è stato autorizzato tramite l'autenticazione Adobe.  <br/>**** Importante: Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.pass.auth) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.pass.<br/>auth) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto:Autorizzato </li> <li> ****<br/> Dati contestuali: (a.media.pass.auth) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pass.auth) </li> </ul> |

### Parte giorno

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: DAY_PART </li> <li> ****<br/> Chiave API: media.dayPart </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> **Valore di esempio:**<br/> </li> <li> ****<br/> Descrizione: Una proprietà che definisce l'ora del giorno in cui il contenuto è stato trasmesso o riprodotto. Questo potrebbe avere qualsiasi valore impostato dai clienti come necessario.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.dayPart) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.dayPart) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto:Parte giorno </li> <li> ****<br/> Dati contestuali: (a.media.dayPart) </li> <li> ****<br/> Feed dati: videodaypart </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.dayPart) </li> </ul> |

### Tipo di feed multimediale

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: FEED </li> <li> ****<br/> Chiave API: media.feed </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 </li> <li> ****<br/> Valore di esempio: "East-HD", "West-HD", "East-SD" </li> <li> ****<br/> Descrizione: Tipo di feed.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.feed) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.feed) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> ****<br/> Nome rapporto: Tipo di feed multimediale </li> <li> ****<br/> Dati contestuali: (a.media.feed) </li> <li> ****<br/> Feed dati: videofeedtype </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.feed) </li> </ul> |

### Artista

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> ****<br/> Chiave API: media.artista </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 <br/>Disponibile in [Media Collection Overview (Panoramica](/help/media-collection-api/mc-api-overview.md) della raccolta multimediale) o [Download SDKs - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> ****<br/> Valore di esempio: "I Beatles" </li> <li> ****<br/> Descrizione: Nome dell'artista.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.artista) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.artista) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> **Nome rapporto:**<br/> </li> <li> ****<br/> Dati contestuali: (a.media.artista) </li> <li> ****<br/> Feed dati: videoaudioartista </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.artista) </li> </ul> |

### Album

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> ****<br/> Chiave API: media.album </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 <br/>Disponibile in [Media Collection Overview (Panoramica](/help/media-collection-api/mc-api-overview.md) della raccolta multimediale) o [Download SDKs - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> ****<br/> Valore di esempio: "Revolver" </li> <li> ****<br/> Descrizione: Nome dell'album.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.album) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.album) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> **Nome rapporto:**<br/> </li> <li> ****<br/> Dati contestuali: (a.media.album) </li> <li> ****<br/> Feed dati: videoaudioalbum </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.album) </li> </ul> |

### Etichetta

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> ****<br/> Chiave API: media.label </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 <br/>Disponibile in [Media Collection Overview (Panoramica](/help/media-collection-api/mc-api-overview.md) della raccolta multimediale) o [Download SDKs - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> ****<br/> Valore di esempio: "Revolver" </li> <li> ****<br/> Descrizione: Nome dell'etichetta del record.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.label) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.label) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> **Nome rapporto:**<br/> </li> <li> ****<br/> Dati contestuali: (a.media.label) </li> <li> ****<br/> Feed dati: videoaudiolibro </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.label) </li> </ul> |

### Autore

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> ****<br/> Chiave API: media.author </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 <br/>Disponibile in [Media Collection Overview (Panoramica](/help/media-collection-api/mc-api-overview.md) della raccolta multimediale) o [Download SDKs - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> ****<br/> Valore di esempio: "John Kennedy Toole" </li> <li> ****<br/> Descrizione: Nome dell’autore (di un audiolibro).  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.author) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.author) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> **Nome rapporto:**<br/> </li> <li> ****<br/> Dati contestuali: (a.media.author) </li> <li> ****<br/> Feed dati: videoaudioautore </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.author) </li> </ul> |

### Stazione

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> ****<br/> Chiave API: media.station </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 <br/>Disponibile in [Media Collection Overview (Panoramica](/help/media-collection-api/mc-api-overview.md) della raccolta multimediale) o [Download SDKs - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> ****<br/> Valore di esempio: "NPR" </li> <li> ****<br/> Descrizione: Nome/ID della stazione radio.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.station) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.station) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> **Nome rapporto:**<br/> </li> <li> ****<br/> Dati contestuali: (a.media.station) </li> <li> ****<br/> Feed dati: videoconferenza </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.station) </li> </ul> |

### Editore

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> ****<br/> Chiave API: media.publisher </li> <li> ****<br/> Obbligatorio: No </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Inizio file multimediali, chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.7 <br/>Disponibile in [Media Collection Overview (Panoramica](/help/media-collection-api/mc-api-overview.md) della raccolta multimediale) o [Download SDKs - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> ****<br/> Valore di esempio: "Random Bauhaus" </li> <li> ****<br/> Descrizione: Nome dell’autore del contenuto audio.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.publisher) </li> <li> ****<br/> Heartbeat: (s:meta:<br/>a.media.publisher) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: eVar </li> <li> ****<br/> Scadenza: HIT </li> <li> **Nome rapporto:**<br/> </li> <li> ****<br/> Dati contestuali: (a.media.publisher) </li> <li> ****<br/> Feed dati: videoaudiopublisher </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.publisher) </li> </ul> |

## Metriche audio e video {#section_3D5F9C555274428AA6030D07596177E9}

###  Inizio file multimediali

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente</li> <li> ****<br/> Chiave API: N/D</li> <li> ****<br/> Tipo: string</li> <li> ****<br/> Inviato con: Media Start</li> <li> **Min.** Versione SDK: Qualsiasi</li> <li> ****<br/> Valore di esempio: TRUE </li> <li> ****<br/> Descrizione: Evento load per il supporto. (Questo si verifica quando il visualizzatore fa clic sul pulsante _Riproduci_ ). Ciò conterebbe anche se ci sono annunci pre-roll, buffering, errori e così via.  <br/>**** Importante: Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.view) </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=start) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: event </li> <li> ****<br/> Nome rapporto: Inizio file multimediali </li> <li> ****<br/> Dati contestuali: (a.media.view) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.view) </li> </ul> |

### Inizio contenuti

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: TRUE </li> <li> ****<br/> Descrizione: Viene utilizzato il primo fotogramma del supporto. Se l'utente cade durante l'annuncio, il buffering, ecc., non ci sarebbe un evento "Inizio contenuto".  <br/> **** Importante: Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: N/D </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: event </li> <li> ****<br/> Nome rapporto: Inizio contenuto </li> <li> ****<br/> Dati contestuali: (a.media.play) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.play) </li> </ul> |

### Content Complete {#content-complete}

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: TRUE </li> <li> ****<br/> Descrizione: Un flusso controllato per il completamento. Ciò non significa necessariamente che l'utente abbia guardato o ascoltato l'intero flusso; avrebbero potuto saltare avanti. Questo significa solo che l'utente ha raggiunto la fine del flusso, 100%. <br/>Vedere anche Fine [](quality-parameters.md#session-end) sessione <br/> **** Importante: Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=complete) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto: Completamento contenuto </li> <li> ****<br/> Dati contestuali: (a.media.complete) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.complete) </li> </ul> |

### Tempo contenuto trascorso

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: 105 </li> <li> ****<br/> Descrizione: Riepiloga la durata dell'evento (in secondi) per tutti gli eventi di tipo PLAY sul contenuto principale.  Il valore verrà visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: N/D </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: event </li> <li> ****<br/> Nome rapporto:Tempo contenuto trascorso </li> <li> ****<br/> Dati contestuali: (a.media.timePlayed) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.timePlayed) </li> </ul> |

###  Tempo contenuto multimediale trascorso

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: 120 </li> <li> ****<br/> Descrizione: Riepiloga la durata dell'evento (in secondi) per tutti gli eventi di tipo PLAY, sia principali che contenuti annuncio.  Il valore verrà visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: N/D </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: event </li> <li> ****<br/> Nome rapporto:Tempo contenuto multimediale trascorso </li> <li> ****<br/> Dati contestuali: (a.media.totalTimePlayed) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### Tempo univoco riprodotto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: 94 </li> <li> ****<br/> Descrizione: Il valore in secondi dei segmenti univoci di contenuto riprodotti durante una sessione. Esclude il tempo di riproduzione negli scenari di ricerca in cui un visualizzatore sta visualizzando più volte lo stesso segmento del contenuto.  Il valore verrà visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: N/D </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: event </li> <li> ****<br/> Nome rapporto: Personalizzato </li> <li> ****<br/> Dati contestuali: (a.media.UniqueTimePlayed) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.UniqueTimePlayed) </li> </ul> |

### Marcatore progresso 10 %

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: TRUE </li> <li> ****<br/> Descrizione: L'indicatore di riproduzione supera il 10% del contenuto in base alla lunghezza. Il marcatore viene conteggiato una sola volta, anche se si cerca all’indietro. Se cercate in avanti, i marcatori saltati non vengono contati.  <br/> **** Importante: Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: N/D </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto: Marcatore progresso 10% </li> <li> ****<br/> Dati contestuali: (a.media.progress10) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress10) </li> </ul> |

### Marcatore progresso 25 %

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: TRUE </li> <li> ****<br/> Descrizione: L'indicatore di riproduzione supera il 25% del contenuto in base alla lunghezza del contenuto. Il marcatore contò solo una volta, anche se cercava all'indietro. Se cercate in avanti, i marcatori saltati non vengono contati.  <br/> **** Importante: Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: N/D </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: event </li> <li> ****<br/> Nome rapporto: Marcatore progresso 25% </li> <li> ****<br/> Dati contestuali: (a.media.progress25) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress25) </li> </ul> |

### Marcatore progresso 50 %

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: TRUE </li> <li> ****<br/> Descrizione: L'indicatore di riproduzione supera il 50% del contenuto in base alla lunghezza del contenuto. Il marcatore contò solo una volta, anche se cercava all'indietro. Se cercate in avanti, i marcatori saltati non vengono contati.  <br/> **** Importante: Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: N/D </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto: Marcatore progresso 50% </li> <li> ****<br/> Dati contestuali: (a.media.progress50) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress50) </li> </ul> |

### Marcatore progresso 75 %

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> **Chiave API:**<br/> **N/D** </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: TRUE </li> <li> ****<br/> Descrizione: L'indicatore di riproduzione supera il 75% del contenuto in base alla lunghezza del contenuto. Il marcatore contò solo una volta, anche se cercava all'indietro. Se cercate in avanti, i marcatori saltati non vengono contati.  <br/> **** Importante: Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: N/D </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: event </li> <li> ****<br/> Nome rapporto: Marcatore progresso 75% </li> <li> ****<br/> Dati contestuali: (a.media.progress75) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress75) </li> </ul> |

### Marcatore progresso 95 %

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: TRUE </li> <li> ****<br/> Descrizione: L'indicatore di riproduzione supera il 95% del contenuto in base alla lunghezza del contenuto. Il marcatore contò solo una volta, anche se cercava all'indietro. Se cercate in avanti, i marcatori saltati non vengono contati.  <br/> **** Importante: Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: N/D </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: event </li> <li> ****<br/> Nome rapporto: Marcatore progresso 95% </li> <li> ****<br/> Dati contestuali: (a.media.progress95) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress95) </li> </ul> |

### Pubblico medio per minuto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: Maggiore o uguale a 1 </li> <li> ****<br/> Descrizione: La metrica Pubblico medio viene calcolata come Tempo contenuto totale trascorso, per un elemento multimediale specifico, diviso per la lunghezza per tutte le sessioni di riproduzione: <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: N/D </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto: Pubblico medio per minuto </li> <li> ****<br/> Dati contestuali: (a.media.averageMinuteAudience) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### Dati federati

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo:boolean </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio:true  </li> <li> ****<br/> Descrizione: Impostato su true quando l’hit è federato (ovvero, ricevuto dal cliente come parte di una condivisione di dati federata, anziché come implementazione). </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: N/D </li> </ul> | <ul> <li> ****<br/> Disponibile: Usa regola di elaborazione personalizzata </li> <li> ****<br/> Variabile riservata: N/D </li> <li> ****<br/> Nome rapporto: N/D </li> <li> ****<br/> Dati contestuali: (a.media.federated) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.federated) </li> </ul> |

### Flussi stimati

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: 1 - Per 19 minuti di riproduzione; <br/>2 - Per 31 minuti di riproduzione; <br/>3 - Per una riproduzione di 78 minuti. </li> <li> ****<br/> Descrizione: Numero stimato di flussi video o audio per ogni singolo contenuto. Questo valore viene aumentato per ogni 30 minuti di tempo di riproduzione (contenuto + annunci). I clienti devono creare le proprie regole di elaborazione per avere il valore disponibile per il reporting. <br/><br/>Un flusso viene conteggiato ogni 30 minuti, in base al `ms_s` (o totalTimePlayed = Video Total Time), simile a: <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: N/D </li> </ul> | <ul> <li> ****<br/> Disponibile: Usa regola di elaborazione personalizzata </li> <li> ****<br/> Variabile riservata: N/D </li> <li> ****<br/> Nome rapporto: Personalizzato </li> <li> ****<br/> Dati contestuali: (a.media.EstimatedStreams) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.EstimStreams) </li> </ul> |

### Flussi interessati in pausa

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.6 </li> <li> ****<br/> Valore di esempio: TRUE </li> <li> ****<br/> Descrizione: Questo valore è vero o falso. È vero se si sono verificate una o più pause durante la riproduzione di un singolo elemento multimediale.  <br/> **** Importante: Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=pause) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto: Flusso interessato sospeso </li> <li> ****<br/> Dati contestuali: (a.media.pause) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pause) </li> </ul> |

###  Pausa eventi

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.6 </li> <li> ****<br/> Valore di esempio: 2 </li> <li> ****<br/> Descrizione: Questa metrica viene calcolata come un conteggio dei periodi di pausa che si sono verificati durante una sessione di riproduzione.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=pause) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: event </li> <li> ****<br/> Nome rapporto: Pausa eventi </li> <li> ****<br/> Dati contestuali: (a.media.pauseCount) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pauseCount) </li> </ul> |

### Durata totale pausa

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.6 </li> <li> ****<br/> Valore di esempio: 190 </li> <li> ****<br/> Descrizione: Riassume la durata (in secondi) di tutti gli eventi di tipo PAUSE. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi. <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: N/D </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata: event </li> <li> ****<br/> Nome rapporto:Durata totale pausa </li> <li> ****<br/> Dati contestuali: (a.media.pauseTime) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pauseTime) </li> </ul> |

###  Riprende contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> **Chiave API:**<br/> **media.curriculum** </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: 1.5.6 </li> <li> ****<br/> Valore di esempio: TRUE </li> <li> ****<br/> Descrizione: Viene conteggiata una ripresa per ogni riproduzione che riprende dopo più di 30 minuti di buffer, pausa o arresto OPPURE se questo valore è impostato dal lettore sul trackPlay di VideoInfo. <br/> **** Importante: Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: (s:event:<br/>type=curriculum) </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto:Riprende contenuto </li> <li> ****<br/> Dati contestuali: (a.media.curriculum) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.curriculum) </li> </ul> |

###  Viste segmento di contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: Imposta automaticamente </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo: string </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: TRUE </li> <li> ****<br/> Descrizione: Numero di visualizzazioni del contenuto principale. Una vista segmento di contenuto viene conteggiata quando viene visualizzato almeno un fotogramma.  <br/> **** Importante: Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore. </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: N/D </li> </ul> | <ul> <li> ****<br/> Disponibile: Yes </li> <li> ****<br/> Variabile riservata:event </li> <li> ****<br/> Nome rapporto:Viste segmento di contenuto </li> <li> ****<br/> Dati contestuali: (a.media.segmentView) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.segmentView) </li> </ul> |

### Conteggio annunci

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: N/D </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: 2 </li> <li> ****<br/> Descrizione: Il numero di annunci avviati durante la sessione multimediale.   <br/> </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: N/D </li> </ul> | <ul> <li> ****<br/> Disponibile: Usa regola di elaborazione personalizzata </li> <li> ****<br/> Variabile riservata: N/D </li> <li> ****<br/> Nome rapporto: Personalizzato </li> <li> ****<br/> Dati contestuali: (a.media.adCount) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.adCount) </li> </ul> |

### Conteggio capitoli

|   Implementazione   | Parametri di rete | Generazione di rapporti   |
| --- | --- | --- |
| <ul> <li> ****<br/> Chiave SDK: N/D </li> <li> ****<br/> Chiave API: N/D </li> <li> ****<br/> Tipo: number </li> <li> ****<br/> Inviato con: Chiusura file multimediali </li> <li> **Min.** Versione SDK: Qualsiasi </li> <li> ****<br/> Valore di esempio: 2 </li> <li> ****<br/> Descrizione: Numero di capitoli avviati durante la sessione per i contenuti multimediali.   <br/> </li></ul> | <ul> <li> ****<br/> Adobe Analytics: N/D </li> <li> ****<br/> Heartbeat: N/D </li> </ul> | <ul> <li> ****<br/> Disponibile: Usa regola di elaborazione personalizzata </li> <li> ****<br/> Variabile riservata: N/D </li> <li> ****<br/> Nome rapporto: Personalizzato </li> <li> ****<br/> Dati contestuali: (a.media.capitoloCount) </li> <li> ****<br/> Feed dati: N/D </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.capitoloCount) </li> </ul> |

## API correlate {#section_Related_APIs}

### API createMediaObject {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### API MediaHeartbeatConfig {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)

