---
title: Parametri audio e video
description: null
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
translation-type: tm+mt
source-git-commit: 4dad6507966e30accfb4f6c2eb5f1d6a5507d29d
workflow-type: tm+mt
source-wordcount: '6234'
ht-degree: 2%

---


# Parametri audio e video{#audio-and-video-parameters}

>[!IMPORTANT]
>
>Il 7 febbraio 2019,  Adobe Analytics per Video e Audio ha rilasciato una modifica al nome della metrica. <i></i>Media Initiates verrà ora denominato <i>Media Starts</i>. Questa modifica è stata apportata per riflettere gli standard di settore nelle metriche e nei report e per rendere la metrica facilmente identificabile nei report.

>[!NOTE]
>
>A partire dal 13 settembre 2018 è stata apportata una modifica alle etichette per alcune dimensioni, metriche e rapporti, per consentire il tracciamento tra contenuti delle analisi video e audio. Le etichette modificate includono: *video avviato* to *i media iniziati*, *lunghezza video* to *lunghezza del contenuto*, and *nome video* to *nome contenuto*. I rapporti video in Reports and Analytics sono stati tutti aggiornati con il nome &quot;File multimediali&quot; anziché &quot;Video&quot;. Le modifiche alle etichette non hanno modificato la raccolta dati o i dati storici. Si prega di prendere nota di queste modifiche nel caso in cui le si stia utilizzando all&#39;interno del Report Builder o in qualsiasi altro prelievo di dati automatizzati esterni che potrebbe essere influenzato da questa modifica.

Questo argomento presenta un elenco di dati di contenuto audio e video, compresi i valori dei dati contestuali, che  Adobe raccoglie tramite variabili della soluzione.

Descrizione dati tabella:

* **Implementazione:** Informazioni su valori e requisiti di implementazione
   * *Key* - Variabile, impostata manualmente nell’app o automaticamente dall’SDK per supporti del Adobe .
   * *Obbligatorio* - Indica se il parametro è richiesto per il tracciamento audio e video di base.
   * *Tipo* - Specifica il tipo di variabile da impostare, stringa o numero.
   * *Inviato con* - Indica quando i dati vengono inviati: *Media Start* è la chiamata di analisi inviata all&#39;avvio del supporto, *Inizio annuncio* è la chiamata di analisi inviata all’inizio dell’annuncio e così via; , *Chiudi* le chiamate sono le chiamate di analisi compilate inviate direttamente dal server heartbeat al server di analisi alla fine della sessione multimediale, o alla fine dell’annuncio, del capitolo e così via. Le chiamate di chiusura non sono disponibili nelle chiamate dei pacchetti di rete.
   * *Min. Versione SDK* - Indica la versione SDK a cui sarà necessario accedere per il parametro.
   * *Valore di esempio* - Fornisce esempi di utilizzo comune delle variabili.
* **Parametri di rete:** Visualizza i valori passati a  server Adobe Analytics o Heartbeat. Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate da  Adobe Media SDK.
* **Reporting:** Informazioni su come visualizzare e analizzare i dati audio e video.
   * *Disponibile* - Indica se i dati sono disponibili nel reporting per impostazione predefinita (*Yes*) o richiede una configurazione personalizzata (*Personalizzato*)
   * *Variabile riservata* - Indica se i dati vengono acquisiti come evento,  eVar, prop o classificazione in una variabile riservata.
   * *Scadenza* - Indica se i dati scadono dopo ogni hit o dopo ogni visita.
   * *Nome rapporto* - Nome del report Analisi  Adobe per la variabile
   * *Dati contestuali* - Nome dei dati contestuali  Adobe Analytics passati al server di reporting e utilizzati nelle regole di elaborazione.
   * *Feed dati* - Nome colonna per la variabile trovata nei feed di dati Clickstream o Live Stream
   * *Audience Manager* - Nome caratteristica trovato in Adobe Audience Manager

>[!IMPORTANT]
>
>Non modificare i nomi delle classificazioni per le variabili elencate di seguito che sono descritte in Reporting/Riservato Variabile come &quot;classificazione&quot;.\
>Le classificazioni dei supporti vengono definite quando una suite di rapporti è abilitata per il tracciamento dei supporti. Di tanto in tanto,  Adobe aggiunge nuove proprietà e, in questo caso, i clienti devono riabilitare le suite di rapporti per accedere alle nuove proprietà del supporto. Durante il processo di aggiornamento  Adobe determina se le classificazioni sono abilitate controllando i nomi delle variabili. Se manca qualcuno di loro,  Adobe aggiunge di nuovo quelli mancanti.

## Dati dei supporti di streaming di base {#core-audio-and-video-data}

### Tipo di flusso {#stream-type}

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media.streamType </li> <li> **Obbligatorio:**<br/> Yes </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 2.2 <br/><br/>Disponibile in [Panoramica API di Media Collection](/help/media-collection-api/mc-api-overview.md) o [Download degli SDK - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> **Valore di esempio:**<br/> &quot;video&quot; </li> <li> **Descrizione:**<br/> Identifica il tipo di flusso. I valori validi sono &quot;audio&quot;, &quot;video&quot; e &quot;.  <br/><br/>[Segmenti di reporting](/help/metrics-and-metadata/segments.md): <br/><br/>Tipo di flusso multimediale: All - <br/>Segmenta tutti i dati del flusso multimediale; Regola: Contenuto (ID) esistente <br/><br/>Tipo di flusso multimediale: Audio - <br/>Segmenta tutti i dati del flusso audio; Regola: Contenuto (ID) esiste e tipo di flusso multimediale = audio <br/><br/>Tipo di flusso multimediale: &quot;Video&quot; - <br/>Segmenta tutti i dati del flusso video; Regola: Il contenuto (ID) esiste e il tipo di flusso multimediale != audio <br/><br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.streamType) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.streamType) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> In visita </li> <li> **Nome rapporto:**<br/> Contenuto </li> <li> **Dati contestuali:**<br/> (a.media.streamType) </li> <li> **Feed dati:**<br/> videostreamtype </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.streamType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media.id </li> <li> **Obbligatorio:**<br/> Yes </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> &quot;4586695ABC&quot; </li> <li>**Descrizione:**<br/> ID contenuto del contenuto, che può essere utilizzato per collegarsi ad altri ID settore/CMS, pari all&#39;ultimo valore di `s:asset:video_id.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.name) </li> <li> **Heartbeat:**<br/> (s:asset:video_id) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> In visita </li> <li> **Nome rapporto:**<br/> Contenuto </li> <li> **Dati contestuali:**<br/> (a.media.name) </li> <li> **Feed dati:**<br/> video </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.name) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType,
                                            MediaHeartbeat.MediaType mediaType)
```

### Lunghezza contenuto (variabile)

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media.length </li> <li> **Obbligatorio:**<br/> Yes </li> <li> **Tipo:**<br/> number </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> VOD: 128; Live: 86400; Lineare: 1800. </li><li> **Descrizione:**<br/> Lunghezza clip/Runtime: lunghezza (o durata) massima del contenuto utilizzato (in secondi). È uguale all&#39;ultimo valore di `l:asset:length` da eventi di tipo Principale. <br/>If `l:asset:length` non è impostato, quindi l&#39;ultimo valore di `l:asset:duration` viene utilizzato. <br/>Nel reporting, Lunghezza video è la classificazione, mentre Lunghezza contenuto (variabile) è il eVar .  <br/> **Importante:** Questa proprietà viene utilizzata per calcolare diverse metriche, come le metriche di tracciamento dell&#39;avanzamento e il pubblico medio in minuti. Se non è impostato o non è maggiore di zero, queste metriche non sono disponibili.  Per i contenuti multimediali live di durata sconosciuta, il valore predefinito è 86400. <br/>Prima della versione 1.5.1, era `l:asset:duration`; dopo la versione 1.5.1 `l:asset:length.` <br/> **Data di rilascio: 13/09/18** </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.length) </li> <li> **Heartbeat:**<br/> (l:asset:length) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> Lunghezza contenuto (variabile) </li> <li> **Dati contestuali:**<br/> (a.media.length) </li> <li> **Feed dati:**<br/> lunghezza video </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType,
                                            MediaHeartbeat.MediaType mediaType)
```

### Lunghezza video

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media.length </li> <li> **Obbligatorio:**<br/> Yes </li> <li> **Tipo:**<br/> number </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> VOD: 128; Live: 86400; Lineare: 1800. </li> <li> **Descrizione:**<br/> Lunghezza clip/Runtime: lunghezza (o durata) massima del contenuto utilizzato (in secondi). È uguale all&#39;ultimo valore di `l:asset:length` da eventi di tipo Principale. If `l:asset:length` non è impostato, quindi l&#39;ultimo valore di `l:asset:duration` viene utilizzato. Nel reporting, Lunghezza video è la classificazione, mentre Lunghezza contenuto (variabile) è il eVar .  <br/> **Importante:** Questa proprietà viene utilizzata per calcolare diverse metriche, come le metriche di tracciamento dell&#39;avanzamento e il pubblico medio in minuti. Se non è impostato o non è maggiore di zero, queste metriche non sono disponibili.  Per i contenuti multimediali live di durata sconosciuta, il valore predefinito è 86400. Prima della versione 1.5.1, era `l:asset:duration`; dopo la versione 1.5.1 `l:asset:length.`<br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.length) </li> <li> **Heartbeat:**<br/> (l:asset:length) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> Lunghezza video </li> <li> **Dati contestuali:**<br/> (a.media.length) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.length) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType,
                                            MediaHeartbeat.MediaType mediaType)
```

### Tipo di contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media.contentType </li> <li> **Obbligatorio:**<br/> Yes </li> <li> **Tipo:**<br/> stringa limitata </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> &quot;vod&quot; </li> <li> **Descrizione:**<br/> Valori disponibili per **Tipo di flusso**: <br/> _Audio:_ &quot;canzone&quot;, &quot;podcast&quot;, &quot;audiobook&quot;, &quot;radio&quot; <br/> _Video:_ &quot;VoD&quot;, &quot;Live&quot;, &quot;Linear&quot;, &quot;UGC&quot;, &quot;DVoD&quot; <br/> I clienti possono fornire valori personalizzati per questo parametro. È uguale a `s:stream:type.` Se questo non è impostato, è uguale a `missing_content_type.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.contentType) </li> <li> **Heartbeat:**<br/> (s:stream:type) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> Tipo di contenuto </li> <li> **Dati contestuali:**<br/> (a.contentType) </li> <li> **Feed dati:**<br/> videocontenttype </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.contentType) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### ID sessione multimediale

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> Ottenuto dal back-end </li> <li> **Obbligatorio:**<br/> Yes </li> <li> **Tipo:**<br/> number </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.8 </li> <li> **Valore di esempio:**<br/> 1482236761294786918253 </li> <li> **Descrizione:**<br/> Questo identifica un&#39;istanza di un flusso di contenuto univoco per una singola riproduzione.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.vsid) </li> <li> **Battito cardiaco:**<br/> (s:event:sid) </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.vsid) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.vsid) </li> </ul> |

### Flag Download Media

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> `config.downloadedcontent` </li> <li> **Chiave API:**<br/> Ottenuto dal back-end </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> boolean </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** <br/>Avvia l&#39;estensione Android e iOS v1.1.0 </li> <li> **Valore di esempio:**<br/> true </li> <li> **Descrizione:**<br/> Impostato su true quando l’hit viene generato a causa della riproduzione di una sessione multimediale di contenuto scaricata. Non presente quando il contenuto scaricato non viene riprodotto.<br/><br/>[Launch](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker-with-optional-configuration)  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.download) </li> <li> **Battito cardiaco:**<br/> (s:meta:a.media.download) </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.download) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.download) </li> </ul> |

### Nome lettore contenuti

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **Chiave API:**<br/> media.playerName </li> <li> **Obbligatorio:**<br/> Yes </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> &quot;Brightcove&quot; </li> <li> **Descrizione:**<br/> Nome del giocatore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>playerName) </li> <li> **Heartbeat:**<br/> (s:sp:player_name) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> Nome lettore contenuti </li> <li> **Dati contestuali:**<br/> (a.media.playerName) </li> <li> **Feed dati:**<br/> videoplayername </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.playerName) </li> </ul> |

### Canale contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **Chiave API:**<br/> media.channel </li> <li> **Obbligatorio:**<br/> Yes </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> &quot;Sport&quot; </li> <li> **Descrizione:**<br/> Stazione di distribuzione/Canali o dove viene riprodotto il contenuto. Qualsiasi valore di stringa è accettato qui.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.channel) </li> <li> **Heartbeat:**<br/> (s:sp:channel) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> Canale contenuto </li> <li> **Dati contestuali:**<br/> (a.media.channel) </li> <li> **Feed dati:**<br/> videocanale </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.channel) </li> </ul> |

### Segmento di contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Yes </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> &quot;0-10&quot; </li> <li> **Descrizione:**<br/> Intervallo che descrive la parte del contenuto visualizzata (in minuti). Il segmento viene calcolato come minimo e massimo dei valori dell&#39;indicatore di riproduzione durante una sessione di riproduzione.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> Segmento di contenuto </li> <li> **Dati contestuali:**<br/> (a.media.segment) </li> <li> **Feed dati:**<br/> videosegmento </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.segment) </li> </ul> |

### Nome contenuto (variabile)

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media.name </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.1 </li> <li> **Valore di esempio:**<br/> &quot;La Teoria del Big Bang&quot; </li> <li> **Descrizione:**<br/> Questo è il nome &quot;descrittivo&quot; (leggibile dall&#39;uomo) del contenuto, uguale all&#39;ultimo valore di `s:asset:name.`<br/>Nel reporting, Nome video è la classificazione e Nome contenuto (variabile) è l&#39;eVar . <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>friendlyName) </li> <li> **Heartbeat:**<br/> (s:asset:name) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> Nome contenuto (variabile) </li> <li> **Dati contestuali:**<br/> (a.media.friendlyName) </li> <li> **Feed dati:**<br/> videoname </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType,
                                            MediaHeartbeat.MediaType mediaType)
```

### Nome del video

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **Chiave API:**<br/> media.name </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.1 </li> <li> **Valore di esempio:**<br/> &quot;La Teoria del Big Bang&quot; </li> <li> **Descrizione:**<br/> Questo è il nome &quot;descrittivo&quot; (leggibile dall&#39;uomo) del contenuto, uguale all&#39;ultimo valore di `s:asset:name.` <br/>Nel reporting, Nome video è la classificazione e Nome contenuto (variabile) è l&#39;eVar .  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>friendlyName) </li> <li> **Heartbeat:**<br/> (s:asset:name) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> Nome video </li> <li> **Dati contestuali:**<br/> (a.media.friendlyName) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

### Percorso video

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> &quot;4586695ABC&quot; </li> <li> **Descrizione:**<br/> Consente di tenere traccia del percorso di un visualizzatore in un sito e/o in un’app, per visualizzare il percorso seguito per visualizzare un particolare video. Qualsiasi combinazione di numeri interi e/o lettere.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.name) </li> <li> **Heartbeat:**<br/> (s:asset:video_id) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> prop </li> <li> **Nome rapporto:**<br/> Percorso video </li> <li> **Dati contestuali:**<br/> (a.media.name) </li> <li> **Feed dati:**<br/> videopath </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.name) </li> </ul> |

### Versione SDK

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **Chiave API:**<br/> media.sdkVersion </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> &quot;2.62.0_release&quot; </li> <li> **Descrizione:**<br/> Versione SDK utilizzata dal lettore. Questo potrebbe avere qualsiasi valore personalizzato che abbia senso per il lettore. <br/><br/>I clienti dovranno creare le proprie regole di elaborazione per avere il valore disponibile per il reporting.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>sdkVersion) </li> <li> **Heartbeat:**<br/> (s:sp:sdk) </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/> (a.media.sdkVersion) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### Versione VHL

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> &quot;js-2.0.1.88-c8c0b1&quot; </li> <li> **Descrizione:**<br/> La versione Media SDK utilizzata per la sessione di tracciamento. <br/><br/>I clienti dovranno creare le proprie regole di elaborazione per avere il valore disponibile per il reporting.  <br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>vhlVersion) </li> <li> **Heartbeat:**<br/> (s:sp:hb_version) </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.vhlVersion) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## Standard Steaming dei metadati dei supporti {#standard-audio-and-video-metadata}

### Mostra le informazioni

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> MOSTRA </li> <li> **Chiave API:**<br/> media.show </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> &quot;Famiglia Moderna&quot; &quot;L&#39;ultima danza&quot; &quot;nuova ragazza&quot; </li> <li> **Descrizione:**<br/> Nome programma/serie <br/>Il nome del programma è obbligatorio solo se la presentazione fa parte di una serie.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.show) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.show) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> Mostra </li> <li> **Dati contestuali:**<br/> (a.media.show) </li> <li> **Feed dati:**<br/> videoshow </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.show) </li> </ul> |

### Formato flusso

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> STREAM_FORMAT </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> &quot;Live&quot; </li> <li> **Descrizione:**<br/> Formato del flusso (Live, VOD, Linear).  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.format) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.format) </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.format) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.format) </li> </ul> |

### Stagione

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> STAGIONE </li> <li> **Chiave API:**<br/> media.season </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> &quot;2&quot; </li> <li> **Descrizione:**<br/> Il numero di stagione a cui appartiene lo spettacolo.  Stagione Serie è richiesto solo se lo show fa parte di una serie.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.stagione) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.stagione) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> Stagione </li> <li> **Dati contestuali:**<br/> (a.media.stagione) </li> <li> **Feed dati:**<br/> videoconferenza </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.stagione) </li> </ul> |

### Episodio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> EPISODE </li> <li> **Chiave API:**<br/> media.episode </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> &quot;13&quot; </li> <li> **Descrizione:**<br/> Numero dell&#39;episodio.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.episode) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.episode) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> Episodio </li> <li> **Dati contestuali:**<br/> (a.media.episode) </li> <li> **Feed dati:**<br/> videoepisodio </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.episode) </li> </ul> |

### ID risorsa

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> ASSET_ID </li> <li> **Chiave API:**<br/> media.assetId </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> &quot;89745363&quot; </li> <li> **Descrizione:**<br/> Questo è l’identificatore univoco per il contenuto della risorsa multimediale, ad esempio l’identificatore episodio della serie TV, l’identificatore della risorsa filmato o l’identificatore evento dal vivo. In genere questi ID sono derivati da autorità di metadati quali EIDR, TMS/Gracenote o Rovi. Questi identificatori possono provenire anche da altri sistemi proprietari o interni.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.asset) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.asset) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> ID risorsa </li> <li> **Dati contestuali:**<br/> (a.media.asset) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.asset) </li> </ul> |

### Genere

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> GENERE </li> <li> **Chiave API:**<br/> media.genre </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> &quot;Drama&quot;, &quot;Comedy&quot; </li> <li> **Descrizione:**<br/> Tipo o raggruppamento di contenuti come definito dal produttore di contenuti. I valori devono essere delimitati da virgole nell’implementazione della variabile. Nel reporting, l&#39;elenco  eVar dividerà ogni valore in un elemento riga, con ogni elemento riga che riceve lo stesso peso delle metriche.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.genre) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.genre) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> Elenco  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> Genere </li> <li> **Dati contestuali:**<br/> (a.media.genre) </li> <li> **Feed dati:**<br/> videogenere </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.genre) </li> </ul> |

### Data primo Air

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> FIRST_AIR_DATE </li> <li> **Chiave API:**<br/> media.firstAirDate </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> &quot;2016-01-25&quot; </li> <li> **Descrizione:**<br/> La data in cui il contenuto è andato in onda per la prima volta in televisione. Qualsiasi formato di data è accettabile, ma  Adobe consiglia: AAAA-MM-GG </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.airDate) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.airDate) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> Data primo Air </li> <li> **Dati contestuali:**<br/> (a.media.airDate) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.airDate) </li> </ul> |

### Prima data digitale

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> FIRST_DIGITAL_DATE </li> <li> **Chiave API:**<br/> media.firstDigitalDate </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> &quot;2016-01-25&quot; </li> <li> **Descrizione:**<br/> Data in cui il contenuto è stato trasmesso per la prima volta su qualsiasi canale o piattaforma digitale. Qualsiasi formato di data è accettabile, ma  Adobe consiglia: AAAA-MM-GG </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.digitalDate) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.digitalDate) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Prima data digitale </li> <li> **Dati contestuali:**<br/> (a.media.digitalDate) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.digitalDate) </li> </ul> |

### Valutazione contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> VALUTAZIONE </li> <li> **Chiave API:**<br/> media.rating </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> TVG, TVG, TVPG, TVMA </li> <li> **Descrizione:**<br/> Classificazione come definita dalle linee guida TV sui genitori.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.rating) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.rating) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Valutazione contenuto </li> <li> **Dati contestuali:**<br/> (a.media.rating) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.rating) </li> </ul> |

### Creatore

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> ORIGINATORE </li> <li> **Chiave API:**<br/> media.originator </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> &quot;Warner Brothers&quot;, &quot;Sony&quot;, &quot;Disney&quot; </li> <li> **Descrizione:**<br/> Creatore del contenuto.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.originator) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.originator) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome rapporto:**<br/> Creatore </li> <li> **Dati contestuali:**<br/> (a.media.originator) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.originator) </li> </ul> |

### Rete 

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> RETE </li> <li> **Chiave API:**<br/> media.network </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> &quot;Fox&quot;, &quot;Bravo&quot;, &quot;ESPN&quot; </li> <li> **Descrizione:**<br/> Nome della rete/del canale.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.network) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.network) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> Rete </li> <li> **Dati contestuali:**<br/> (a.media.network) </li> <li> **Feed dati:**<br/> videonetwork </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.network) </li> </ul> |

### Mostra tipo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> SHOW_TYPE </li> <li> **Chiave API:**<br/> media.showType </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> &quot;0&quot; = episodio completo; &quot;1&quot; = Anteprima/trailer; &quot;2&quot; = Clip; &quot;3&quot; = Altro. </li> <li> **Descrizione:**<br/> Tipo di contenuto, espresso come numero intero compreso tra 0 e 3.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.type) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.type) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> Mostra tipo </li> <li> **Dati contestuali:**<br/> (a.media.type) </li> <li> **Feed dati:**<br/> videoshowtype </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> MVPD </li> <li> **Chiave API:**<br/> media.pass.mvpd </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> &quot;Comcast&quot;, &quot;DirectTV&quot;, &quot;Dish&quot; </li> <li> **Descrizione:**<br/> MVPD fornito tramite l&#39;autenticazione  Adobe.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.pass.mvpd) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.pass.<br/>mvpd) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> MVPD </li> <li> **Dati contestuali:**<br/> (a.media.pass.mvpd) </li> <li> **Feed dati:**<br/> videomvpd </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### Autorizzato

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> AUTORIZZATO </li> <li> **Chiave API:**<br/> media.pass.auth </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> &quot;TRUE&quot; </li> <li> **Descrizione:**<br/> L&#39;utente è stato autorizzato tramite l&#39;autenticazione  Adobe.  <br/>**Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.pass.auth) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.pass.<br/>auth) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Autorizzato </li> <li> **Dati contestuali:**<br/> (a.media.pass.auth) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.pass.auth) </li> </ul> |

### Parte giorno

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> DAY_PART </li> <li> **Chiave API:**<br/> media.dayPart </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> </li> <li> **Descrizione:**<br/> Una proprietà che definisce l&#39;ora del giorno in cui il contenuto è stato trasmesso o riprodotto. Questo potrebbe avere qualsiasi valore impostato dai clienti come necessario.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.dayPart) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.dayPart) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> Parte giorno </li> <li> **Dati contestuali:**<br/> (a.media.dayPart) </li> <li> **Feed dati:**<br/> videodaypart </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.dayPart) </li> </ul> |

### Tipo di feed multimediale

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> FEED </li> <li> **Chiave API:**<br/> media.feed </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 </li> <li> **Valore di esempio:**<br/> &quot;East-HD&quot;, &quot;West-HD&quot;, &quot;East-SD&quot; </li> <li> **Descrizione:**<br/> Tipo di feed.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.feed) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.feed) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> Tipo di feed multimediale </li> <li> **Dati contestuali:**<br/> (a.media.feed) </li> <li> **Feed dati:**<br/> videofeedtype </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.feed) </li> </ul> |

### Artista

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.artista </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 <br/>Disponibile in [Panoramica della raccolta di file multimediali](/help/media-collection-api/mc-api-overview.md) o [Download degli SDK - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> &quot;I Beatles&quot; </li> <li> **Descrizione:**<br/> Nome dell&#39;artista.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.artista) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.artista) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/> (a.media.artista) </li> <li> **Feed dati:**<br/> videoaudioartista </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.artista) </li> </ul> |

### Album

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.album </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 <br/>Disponibile in [Panoramica della raccolta di file multimediali](/help/media-collection-api/mc-api-overview.md) o [Download degli SDK - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> &quot;Revolver&quot; </li> <li> **Descrizione:**<br/> Nome dell&#39;album.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.album) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.album) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/> (a.media.album) </li> <li> **Feed dati:**<br/> videoaudioalbum </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.album) </li> </ul> |

### Etichetta

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.label </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 <br/>Disponibile in [Panoramica della raccolta di file multimediali](/help/media-collection-api/mc-api-overview.md) o [Download degli SDK - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> &quot;Revolver&quot; </li> <li> **Descrizione:**<br/> Nome dell&#39;etichetta del record.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.label) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.label) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/> (a.media.label) </li> <li> **Feed dati:**<br/> videoaudiolibro </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.label) </li> </ul> |

### Autore

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.author </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 <br/>Disponibile in [Panoramica della raccolta di file multimediali](/help/media-collection-api/mc-api-overview.md) o [Download degli SDK - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> &quot;John Kennedy Toole&quot; </li> <li> **Descrizione:**<br/> Nome dell’autore (di un audiolibro).  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.author) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.author) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/> (a.media.author) </li> <li> **Feed dati:**<br/> videoaudioautore </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.author) </li> </ul> |

### Stazione

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.station </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 <br/>Disponibile in [Panoramica della raccolta di file multimediali](/help/media-collection-api/mc-api-overview.md) o [Download degli SDK - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> &quot;NPR&quot; </li> <li> **Descrizione:**<br/> Nome/ID della stazione radio.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.station) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.station) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/> (a.media.station) </li> <li> **Feed dati:**<br/> videoaudiostazione </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.station) </li> </ul> |

### Editore

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.publisher </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Inizio file multimediali, chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.7 <br/>Disponibile in [Panoramica della raccolta di file multimediali](/help/media-collection-api/mc-api-overview.md) o [Download degli SDK - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> &quot;Random Bauhaus&quot; </li> <li> **Descrizione:**<br/> Nome dell’autore del contenuto audio.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.publisher) </li> <li> **Heartbeat:**<br/> (s:meta:<br/>a.media.publisher) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> Su HIT </li> <li> **Nome rapporto:**<br/> </li> <li> **Dati contestuali:**<br/> (a.media.publisher) </li> <li> **Feed dati:**<br/> videoaudiopublisher </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.publisher) </li> </ul> |

## Metriche per contenuti multimediali in streaming {#audio-and-video-metrics}

### Inizio file multimediali

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente</li> <li> **Chiave API:**<br/> N/D</li> <li> **Tipo:**<br/> string</li> <li> **Inviato con:**<br/> Media Start</li> <li> **Min. Versione SDK:** Qualsiasi</li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Evento load per il supporto. (Questo si verifica quando il visualizzatore fa clic sul pulsante _Riproduci_ button). Ciò conterebbe anche se ci sono annunci pre-roll, buffering, errori e così via.  <br/>**Importante:**  Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.view) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=start) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Inizio file multimediali </li> <li> **Dati contestuali:**<br/> (a.media.view) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.view) </li> </ul> |

### Inizio contenuti

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Viene utilizzato il primo fotogramma del supporto. Se l&#39;utente cade durante l&#39;annuncio, il buffering, ecc., non ci sarebbe un evento &quot;Inizio contenuto&quot;.  <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Inizio contenuto </li> <li> **Dati contestuali:**<br/> (a.media.play) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.play) </li> </ul> |

### Content Complete {#content-complete}

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Un flusso controllato per il completamento. Ciò non significa necessariamente che l&#39;utente abbia guardato o ascoltato l&#39;intero flusso; avrebbero potuto saltare avanti. Ciò significa solo che l&#39;utente ha raggiunto la fine del flusso, pari al 100%. <br/>Consulta anche [Fine sessione](quality-parameters.md#session-end) <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=complete) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Completamento contenuto </li> <li> **Dati contestuali:**<br/> (a.media.complete) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.complete) </li> </ul> |

### Tempo contenuto trascorso

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> number </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 105 </li> <li> **Descrizione:**<br/> Riepiloga la durata dell&#39;evento (in secondi) per tutti gli eventi di tipo PLAY sul contenuto principale.  Il valore verrà visualizzato nel formato ora (HH:MM:SS) in  Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Tempo contenuto trascorso </li> <li> **Dati contestuali:**<br/> (a.media.timePlayed) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.timePlayed) </li> </ul> |

### Tempo contenuto multimediale trascorso

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> number </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 120 </li> <li> **Descrizione:**<br/> Riepiloga la durata dell&#39;evento (in secondi) per tutti gli eventi di tipo PLAY, sia principali che contenuti annuncio.  Il valore verrà visualizzato nel formato ora (HH:MM:SS) in  Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Tempo contenuto multimediale trascorso </li> <li> **Dati contestuali:**<br/> (a.media.totalTimePlayed) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### Tempo univoco riprodotto

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> number </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 94 </li> <li> **Descrizione:**<br/> Il valore in secondi dei segmenti univoci di contenuto riprodotti durante una sessione. Esclude il tempo di riproduzione negli scenari di ricerca in cui un visualizzatore sta visualizzando più volte lo stesso segmento del contenuto.  Il valore verrà visualizzato nel formato ora (HH:MM:SS) in  Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.UniqueTimePlayed) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.UniqueTimePlayed) </li> </ul> |

### Marcatore progresso 10 %

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> L&#39;indicatore di riproduzione supera il 10% del contenuto in base alla lunghezza. Il marcatore viene conteggiato una sola volta, anche se si cerca all’indietro. Se cercate in avanti, i marcatori saltati non vengono conteggiati.  <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Marcatore progresso 10% </li> <li> **Dati contestuali:**<br/> (a.media.progress10) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.progress10) </li> </ul> |

### Marcatore progresso 25 %

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> La testina di riproduzione supera il marcatore del 25% del contenuto in base alla lunghezza del contenuto. Il marcatore contò solo una volta, anche se cercava all&#39;indietro. Se cercate in avanti, i marcatori saltati non vengono conteggiati.  <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Marcatore progresso 25% </li> <li> **Dati contestuali:**<br/> (a.media.progress25) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.progress25) </li> </ul> |

### Marcatore progresso 50 %

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> L&#39;indicatore di riproduzione supera il 50% del contenuto in base alla lunghezza del contenuto. Il marcatore contò solo una volta, anche se cercava all&#39;indietro. Se cercate in avanti, i marcatori saltati non vengono conteggiati.  <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Marcatore progresso 50% </li> <li> **Dati contestuali:**<br/> (a.media.progress50) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.progress50) </li> </ul> |

### Marcatore progresso 75 %

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> **N/D** </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> La testina di riproduzione supera il marcatore del 75% del contenuto in base alla lunghezza del contenuto. Il marcatore contò solo una volta, anche se cercava all&#39;indietro. Se cercate in avanti, i marcatori saltati non vengono conteggiati.  <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Marcatore progresso 75% </li> <li> **Dati contestuali:**<br/> (a.media.progress75) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.progress75) </li> </ul> |

### Marcatore progresso 95 %

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> La testina di riproduzione supera il marcatore del 95% del contenuto in base alla lunghezza del contenuto. Il marcatore contò solo una volta, anche se cercava all&#39;indietro. Se cercate in avanti, i marcatori saltati non vengono conteggiati.  <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Marcatore progresso 95% </li> <li> **Dati contestuali:**<br/> (a.media.progress95) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.progress95) </li> </ul> |

### Pubblico medio per minuto

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> number </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> Maggiore o uguale a 1 </li> <li> **Descrizione:**<br/> La metrica Pubblico medio viene calcolata come Tempo contenuto totale trascorso, per un elemento multimediale specifico, diviso per la lunghezza per tutte le sessioni di riproduzione: <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Pubblico medio per minuto </li> <li> **Dati contestuali:**<br/> (a.media.averageMinuteAudience) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### Secondi dall’ultima chiamata

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> number </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 600</li> <li> **Descrizione:**<br/> La metrica secondi dall’ultima chiamata è 0 se il flusso è stato chiuso con un evento complete o con un evento finale e in genere è 600 se è stato chiuso a causa di timeout. Questa metrica non dispone di una variabile di soluzione e di regole di elaborazione automatica, pertanto devi creare una regola di elaborazione personalizzata per salvarla.</li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> N/D </li> <li> **Dati contestuali:**<br/> (a.media.secondiSinceLastCall) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.secondiSinceLastCall) </li> </ul> |

### Dati federati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> boolean </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> true  </li> <li> **Descrizione:**<br/> Impostato su true quando l’hit è federato (ovvero, ricevuto dal cliente come parte di una condivisione di dati federata, anziché come implementazione). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> N/D </li> <li> **Dati contestuali:**<br/> (a.media.federated) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.federated) </li> </ul> |

### Flussi stimati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> number </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 1 - Per 19 minuti di riproduzione; <br/>2 - Per 31 minuti di riproduzione; <br/>3 - Per una riproduzione di 78 minuti. </li> <li> **Descrizione:**<br/> Numero stimato di flussi video o audio per ogni singolo contenuto. Questo valore viene aumentato per ogni 30 minuti di tempo di riproduzione (contenuto + annunci). I clienti devono creare le proprie regole di elaborazione per avere il valore disponibile per il reporting. <br/><br/>Un flusso viene conteggiato ogni 30 minuti, in base al `ms_s` (o totalTimePlayed = Video Total Time), simile a: <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.EstimatedStreams) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.EstimStreams) </li> </ul> |

### Flussi interessati in pausa

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.6 </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Questo valore è vero o falso. È vero se si sono verificate una o più pause durante la riproduzione di un singolo elemento multimediale.  <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Flusso interessato sospeso </li> <li> **Dati contestuali:**<br/> (a.media.pause) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.pause) </li> </ul> |

### Pausa eventi

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> number </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.6 </li> <li> **Valore di esempio:**<br/> 2 </li> <li> **Descrizione:**<br/> Questa metrica viene calcolata come un conteggio dei periodi di pausa che si sono verificati durante una sessione di riproduzione.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Pausa eventi </li> <li> **Dati contestuali:**<br/> (a.media.pauseCount) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.pauseCount) </li> </ul> |

### Durata totale pausa

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> number </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.6 </li> <li> **Valore di esempio:**<br/> 190 </li> <li> **Descrizione:**<br/> Riassume la durata (in secondi) di tutti gli eventi di tipo PAUSE. Il valore verrà visualizzato nel formato ora (HH:MM:SS) in  Analysis Workspace e Reporting e analisi. Nelle API Feed dati, Data Warehouse e Reporting i valori verranno visualizzati in secondi. <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Durata totale pausa </li> <li> **Dati contestuali:**<br/> (a.media.pauseTime) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.pauseTime) </li> </ul> |

### Riprende contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> **media.curriculum** </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** 1.5.6 </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Viene conteggiata una ripresa per ogni riproduzione che riprende dopo più di 30 minuti di buffer, pausa o arresto OPPURE se questo valore è impostato dal lettore sul trackPlay di VideoInfo. <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=curriculum) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Riprende contenuto </li> <li> **Dati contestuali:**<br/> (a.media.curriculum) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.curriculum) </li> </ul> |

### Viste segmento di contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Numero di visualizzazioni del contenuto principale. Una vista segmento di contenuto viene conteggiata quando viene visualizzato almeno un fotogramma.  <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore. </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome rapporto:**<br/> Viste segmento di contenuto </li> <li> **Dati contestuali:**<br/> (a.media.segmentView) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.segmentView) </li> </ul> |


### Conteggio annunci

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> N/D </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> number </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 2 </li> <li> **Descrizione:**<br/> Il numero di annunci avviati durante la sessione multimediale.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.adCount) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.adCount) </li> </ul> |

### Conteggio capitoli

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> N/D </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> number </li> <li> **Inviato con:**<br/> Chiusura file multimediali </li> <li> **Min. Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 2 </li> <li> **Descrizione:**<br/> Numero di capitoli avviati durante la sessione per i contenuti multimediali.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Heartbeat:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome rapporto:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.capitoloCount) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager :**<br/> (c_contextdata.<br/>a.media.capitoloCount) </li> </ul> |


## Parametri del California Consumer Privacy Act (CCPA) {#ccpa-params}

### Avviamento lato server di rifiuto

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> N/D </li> <li> **Chiave API:**<br/> analytics.optOutServerSideForwarding </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> boolean </li> <li> **Inviato con:**<br/> Media Start </li> <li> **Min. Versione SDK:** N/D </li> <li> **Valore di esempio:**<br/> true </li> <li>**Descrizione:**<br/> Impostato su true quando l&#39;utente finale ha rinunciato a condividere i propri dati tra  Adobe Analytics e altre soluzioni  Experienci Cloud (ad es.  Audience Manager). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (opt.dmp) </li> <li> **Heartbeat:**<br/> (s:meta:cm.ssf) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> In visita </li> <li> **Nome rapporto:**<br/> Contenuto </li> <li> **Dati contestuali:**<br/> N/D </li> <li> **Feed dati:**<br/> video </li> <li> **Audience Manager :**<br/> N/D </li> </ul> |

### Opzione di rifiuto

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> N/D </li> <li> **Chiave API:**<br/> analytics.optOutShare </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> boolean </li> <li> **Inviato con:**<br/> Media Start </li> <li> **Min. Versione SDK:** N/D </li> <li> **Valore di esempio:**<br/> true </li> <li>**Descrizione:**<br/> Impostato su true quando l&#39;utente finale ha rinunciato alla federazione dei propri dati (ad es. ad altri client Adobe Analytics ). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (opt.oos) </li> <li> **Heartbeat:**<br/> (s:meta:cm.oos) </li> </ul> | <ul> <li> **Disponibile:**<br/> Yes </li> <li> **Variabile riservata:**<br/>  eVar </li> <li> **Scadenza:**<br/> In visita </li> <li> **Nome rapporto:**<br/> Contenuto </li> <li> **Dati contestuali:**<br/> N/D </li> <li> **Feed dati:**<br/> video </li> <li> **Audience Manager :**<br/> N/D </li> </ul> |

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
