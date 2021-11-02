---
title: Parametri audio e video
description: Scopri le variabili di dati di Core Streaming Media, compresi i dati di contenuto audio e video e i valori di dati contestuali.
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
exl-id: 9dc84377-6eca-482f-89e7-c4008d1c0f07
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 37c46d493926ab83d9b6ccedafd82b150bbd6e2c
workflow-type: tm+mt
source-wordcount: '6488'
ht-degree: 2%

---

# Parametri audio e video{#audio-and-video-parameters}

Questo argomento presenta un elenco di dati di contenuto audio e video, compresi i valori dei dati di contesto, che l’Adobe raccoglie tramite variabili della soluzione.

>[!IMPORTANT]
>
>Il 7 febbraio 2019, Adobe Analytics for Video and Audio ha rilasciato una modifica al nome di una metrica. <i></i>Media Initiates verrà ora denominato <i>Media Starts</i>. Questa modifica è stata apportata per riflettere gli standard di settore nelle metriche e nei rapporti e per rendere la metrica facilmente identificabile nei rapporti.

>[!NOTE]
>
>A partire dal 13 settembre 2018 è stata apportata una modifica alle etichette per alcune dimensioni, metriche e rapporti, per consentire il tracciamento tra contenuti di analisi video e audio. Le etichette modificate includono: *il video si avvia* a *media Initiates*, *lunghezza video* a *lunghezza del contenuto* e *nome video* a *nome del contenuto*. I rapporti video in Reports and Analytics sono stati tutti aggiornati con il nome &quot;Media&quot; anziché &quot;Video&quot;. Le modifiche dell’etichetta non hanno modificato la raccolta dati o i dati storici. Tieni presente queste modifiche nel caso in cui le utilizzi all’interno del Report Builder o in qualsiasi altro richiamo di dati automatizzato esterno che potrebbe essere influenzato da questa modifica.

Descrizione dei dati della tabella:

* **Implementazione:** Informazioni su valori e requisiti di implementazione
   * *Chiave* - Variabile, impostata manualmente nell’app o automaticamente dall’SDK di Adobe Medium.
   * *Obbligatorio* - Indica se il parametro è necessario per il tracciamento audio e video di base.
   * *Tipo* - Specifica il tipo di variabile da impostare, stringa o numero.
   * *Inviato con* - Indica quando i dati vengono inviati: *Media Start* è la chiamata di analytics inviata all&#39;avvio del supporto, *Inizio annuncio* è la chiamata di analytics inviata all’inizio dell’annuncio e così via; la *Chiudi* le chiamate sono le chiamate analytics compilate inviate direttamente dal server heartbeat al server analytics alla fine della sessione multimediale, o la fine dell&#39;annuncio, del capitolo, ecc. Le chiamate di chiusura non sono disponibili nelle chiamate dei pacchetti di rete.
   * *Min Versione SDK* - Indica la versione SDK necessaria per accedere al parametro .
   * *Valore di esempio* - Fornisce un esempio di utilizzo comune delle variabili.
* **Parametri di rete:** Visualizza i valori passati ai server Adobe Analytics o Heartbeat. Questa colonna mostra i nomi dei parametri visualizzati nelle chiamate di rete generate dagli SDK di Adobe Medium.
* **Generazione rapporti:** Informazioni su come visualizzare e analizzare i dati audio e video.
   * *Disponibile* - Indica se i dati sono disponibili nel reporting per impostazione predefinita (*Sì*) o richiede la configurazione personalizzata (*Personalizzato*)
   * *Variabile riservata* - Indica se i dati vengono acquisiti come evento, eVar, prop o classificazione in una variabile riservata.
   * *Scadenza* - Indica se i dati scadono dopo ogni hit o dopo ogni visita.
   * *Nome del rapporto* - Nome del report Adobe Analytics per la variabile
   * *Dati contestuali* - Nome dei dati contestuali di Adobe Analytics passati al server di reporting e utilizzati nelle regole di elaborazione.
   * *Feed di dati* - Nome della colonna per la variabile trovata nei feed di dati Clickstream o Live Stream
   * *Audience Manager* - Nome delle caratteristiche trovato in Adobe Audience Manager

>[!IMPORTANT]
>
>Non modificare i nomi delle classificazioni per le variabili elencate di seguito descritte in Reporting/Riservato Variable come &quot;classificazione&quot;.\
>Le classificazioni per i file multimediali vengono definite quando una suite di rapporti è abilitata per il tracciamento dei contenuti multimediali. Di tanto in tanto, Adobe aggiunge nuove proprietà e, in questo caso, i clienti devono riabilitare le suite di rapporti per accedere alle nuove proprietà multimediali. Durante il processo di aggiornamento, l’Adobe determina se le classificazioni sono abilitate controllando i nomi delle variabili. Se manca qualcuno di questi, Adobe aggiunge di nuovo quelli mancanti.

## Dati multimediali core in streaming {#core-audio-and-video-data}

### Tipo di flusso {#stream-type}

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [mediaType](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media.streamType </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 2.2. <br/><br/>Disponibile in [Panoramica API di Media Collection](/help/media-collection-api/mc-api-overview.md) o [Download degli SDK - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li>  <li> **Valore di esempio:**<br/> &quot;video&quot; </li> <li> **Descrizione:**<br/> Identifica il tipo di flusso. I valori validi sono &quot;audio&quot;, &quot;video&quot; e &quot; &quot;.  <br/><br/>[Segmenti di reporting](/help/metrics-and-metadata/segments.md): <br/><br/>Tipo di flusso multimediale: Tutto - <br/>Segmenta tutti i dati del flusso multimediale; Regola: Contenuto (ID) esistente <br/><br/>Tipo di flusso multimediale: Audio - <br/>Segmenta tutti i dati del flusso audio; Regola: Contenuto (ID) esiste e tipo flusso multimediale = audio <br/><br/>Tipo di flusso multimediale: &quot;Video&quot; - <br/>Segmenta tutti i dati del flusso video; Regola: Contenuto (ID) esiste e tipo flusso multimediale != audio <br/><br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.streamType) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.streamType) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Tipo di flusso </li> <li> **Dati contestuali:**<br/> (a.media.streamType) </li> <li> **Feed dati:**<br/> videostreamtype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.streamType) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.streamType </li> </ul> |

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
| <ul> <li> **Chiave SDK:**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media.id </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> &quot;4586695ABC&quot; </li> <li>**Descrizione:**<br/> ID contenuto, che può essere utilizzato per ricollegare ad altri ID settore/CMS, uguale all’ultimo valore di `s:asset:video_id.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.name) </li> <li> **Battiti cardiaci:**<br/> s:asset:video_id) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> In visita </li> <li> **Nome report:**<br/> Contenuto </li> <li> **Dati contestuali:**<br/> (a.media.name) </li> <li> **Feed dati:**<br/> video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.name) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType,
                                            MediaHeartbeat.MediaType mediaType)
```

### Lunghezza del contenuto (variabile)

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media.length </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> VOD: 128; Live: 86400; Lineare: 1800. </li><li> **Descrizione:**<br/> Lunghezza clip/Runtime: lunghezza massima (o durata) del contenuto utilizzato (in secondi). È uguale all’ultimo valore di `l:asset:length` da eventi di tipo Main. <br/>Se `l:asset:length` non è impostato, quindi l&#39;ultimo valore di `l:asset:duration` viene utilizzato. <br/>Nel rapporto, Lunghezza video è la classificazione e Lunghezza contenuto (variabile) è l’eVar.  <br/> **Importante:** Questa proprietà viene utilizzata per calcolare diverse metriche, come le metriche di tracciamento dell&#39;avanzamento e il pubblico medio in minuti. Se non è impostato o non è maggiore di zero, queste metriche non sono disponibili.  Per gli elementi multimediali in tempo reale di durata sconosciuta, il valore predefinito è 86400. <br/>Prima della versione 1.5.1, era `l:asset:duration`; dopo la versione 1.5.1, è `l:asset:length.` <br/> **Data di rilascio: 13/09/18** </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.length) </li> <li> **Battiti cardiaci:**<br/> l:asset:lunghezza) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Lunghezza del contenuto (variabile) </li> <li> **Dati contestuali:**<br/> (a.media.length) </li> <li> **Feed dati:**<br/> lunghezza di video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.length) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.xmpDM:duration </li> </ul> |

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
| <ul> <li> **Chiave SDK:**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media.length </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> VOD: 128; Live: 86400; Lineare: 1800. </li> <li> **Descrizione:**<br/> Lunghezza clip/Runtime: lunghezza massima (o durata) del contenuto utilizzato (in secondi). È uguale all’ultimo valore di `l:asset:length` da eventi di tipo Main. Se `l:asset:length` non è impostato, quindi l&#39;ultimo valore di `l:asset:duration` viene utilizzato. Nel rapporto, Lunghezza video è la classificazione e Lunghezza contenuto (variabile) è l’eVar.  <br/> **Importante:** Questa proprietà viene utilizzata per calcolare diverse metriche, come le metriche di tracciamento dell&#39;avanzamento e il pubblico medio in minuti. Se non è impostato o non è maggiore di zero, queste metriche non sono disponibili.  Per gli elementi multimediali in tempo reale di durata sconosciuta, il valore predefinito è 86400. Prima della versione 1.5.1, era `l:asset:duration`; dopo la versione 1.5.1, è `l:asset:length.`<br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.length) </li> <li> **Battiti cardiaci:**<br/> l:asset:lunghezza) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Lunghezza video </li> <li> **Dati contestuali:**<br/> (a.media.length) </li> <li> **Feed dati:**<br/> video.videoclassificationlength </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.length) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.xmpDM:duration </li> </ul> |

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
| <ul> <li> **Chiave SDK:**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media.contentType </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> stringa limitata </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> &quot;vod&quot; </li> <li> **Descrizione:**<br/> Valori disponibili per **Tipo di flusso**: <br/> _Audio:_ &quot;canzone&quot;, &quot;podcast&quot;, &quot;audiolibro&quot;, &quot;radio&quot; <br/> _Video:_ &quot;VoD&quot;, &quot;Live&quot;, &quot;Lineare&quot;, &quot;UGC&quot;, &quot;DVoD&quot; <br/> I clienti possono fornire valori personalizzati per questo parametro. È uguale a `s:stream:type.` Se non viene impostato, è uguale a `missing_content_type.` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.contentType) </li> <li> **Battiti cardiaci:**<br/> s:stream:tipo) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Tipo di contenuto </li> <li> **Dati contestuali:**<br/> (a.contentType) </li> <li> **Feed dati:**<br/> videocontenttype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.contentType) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.broadcastContentType </li> </ul> |

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
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> Ottenuto dal backend </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1.5.8. </li> <li> **Valore di esempio:**<br/> 1482236761294786918253 </li> <li> **Descrizione:**<br/> Questo identifica un&#39;istanza di un flusso di contenuto univoco per una singola riproduzione.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.vsid) </li> <li> **Heartbeat:**<br/> s:event:sid) </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome report:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.vsid) </li> <li> **Feed dati:**<br/> videosess ionid </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vsid) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.@id </li> </ul> |

### Flag scaricato contenuto multimediale

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> `config.downloadedcontent` </li> <li> **Chiave API:**<br/> Ottenuto dal backend </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> booleano </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** <br/>Launch Estensione Android e iOS v1.1.0 </li> <li> **Valore di esempio:**<br/> true </li> <li> **Descrizione:**<br/> Impostato su true quando l&#39;hit viene generato a causa della riproduzione di una sessione multimediale di contenuto scaricato. Non presente quando il contenuto scaricato non viene riprodotto.<br/><br/>[Launch](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker-with-optional-configuration)  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.scaricato) </li> <li> **Heartbeat:**<br/> s:meta:a.media.download) </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome report:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.scaricato) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.download) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.scaricatoPlayback </li> </ul> |

### Nome del lettore di contenuti

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **Chiave API:**<br/> media.playerName </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> &quot;Brightcove&quot; </li> <li> **Descrizione:**<br/> Nome del lettore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>playerName) </li> <li> **Battiti cardiaci:**<br/> s:sp:player_name) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Nome del lettore di contenuti </li> <li> **Dati contestuali:**<br/> (a.media.playerName) </li> <li> **Feed dati:**<br/> videoplayname </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.playerName) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.playerName </li> </ul> |

### Canale del contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **Chiave API:**<br/> media.channel </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> &quot;Sport&quot; </li> <li> **Descrizione:**<br/> Stazione di distribuzione/canali o dove viene riprodotto il contenuto. Qualsiasi valore stringa è accettato qui.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.channel) </li> <li> **Battiti cardiaci:**<br/> s:sp:canale) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Canale del contenuto </li> <li> **Dati contestuali:**<br/> (a.media.channel) </li> <li> **Feed dati:**<br/> canale video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.channel) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.broadcastChannel </li> </ul> |

### Segmento di contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> Sì </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> &quot;0-10&quot; </li> <li> **Descrizione:**<br/> Intervallo che descrive la parte del contenuto visualizzata (in minuti). Il segmento viene calcolato come minimo e massimo dei valori della testina di riproduzione durante una sessione di riproduzione.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Segmento di contenuto </li> <li> **Dati contestuali:**<br/> (a.media.segment) </li> <li> **Feed dati:**<br/> videosegmento </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.segment) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value </li> </ul> |

### Nome contenuto (variabile)

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **Chiave API:**<br/> media.name </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1.5.1. </li> <li> **Valore di esempio:**<br/> &quot;La teoria del Big Bang&quot; </li> <li> **Descrizione:**<br/> Questo è il nome &quot;descrittivo&quot; (leggibile dall’uomo) del contenuto, uguale all’ultimo valore di `s:asset:name.`<br/>Nel rapporto, Nome video è la classificazione e Nome contenuto (variabile) è l’eVar. <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>friendlyName) </li> <li> **Battiti cardiaci:**<br/> s:asset:nome) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Nome contenuto (variabile) </li> <li> **Dati contestuali:**<br/> (a.media.friendlyName) </li> <li> **Feed dati:**<br/> videoname </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.friendlyName) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.dc:title </li> </ul> |

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
| <ul> <li> **Chiave SDK:**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **Chiave API:**<br/> media.name </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1.5.1. </li> <li> **Valore di esempio:**<br/> &quot;La teoria del Big Bang&quot; </li> <li> **Descrizione:**<br/> Questo è il nome &quot;descrittivo&quot; (leggibile dall’uomo) del contenuto, uguale all’ultimo valore di `s:asset:name.` <br/>Nel rapporto, Nome video è la classificazione e Nome contenuto (variabile) è l’eVar.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>friendlyName) </li> <li> **Battiti cardiaci:**<br/> s:asset:nome) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Nome video </li> <li> **Dati contestuali:**<br/> (a.media.friendlyName) </li> <li> **Feed dati:**<br/> video.videoclassificationname </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.friendlyName) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.dc:title </li> </ul> |

### Percorso video

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> &quot;4586695ABC&quot; </li> <li> **Descrizione:**<br/> Consente di tenere traccia del percorso di un visualizzatore in un sito e/o in un’app, per visualizzare il percorso seguito per visualizzare un video specifico. Qualsiasi combinazione di numeri interi e/o lettere.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.name) </li> <li> **Battiti cardiaci:**<br/> s:asset:video_id) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> prop </li> <li> **Nome report:**<br/> Percorso video </li> <li> **Dati contestuali:**<br/> (a.media.name) </li> <li> **Feed dati:**<br/> videopath </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.name) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier </li> </ul> |

### Versione SDK

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **Chiave API:**<br/> media.sdkVersion </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> &quot;2.62.0_release&quot; </li> <li> **Descrizione:**<br/> Versione SDK utilizzata dal lettore. Questo potrebbe avere qualsiasi valore personalizzato che abbia senso per il tuo lettore. <br/><br/>I clienti dovranno creare le proprie regole di elaborazione per disporre del valore disponibile per il reporting.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>sdkVersion) </li> <li> **Battiti cardiaci:**<br/> s:sp:sdk) </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome report:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.sdkVersion) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.sdkVersion) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version </li> </ul> |

### Versione VHL

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> &quot;js-2.0.1.88-c8c0b1&quot; </li> <li> **Descrizione:**<br/> Versione Media SDK utilizzata per la sessione di tracciamento. <br/><br/>I clienti dovranno creare le proprie regole di elaborazione per disporre del valore disponibile per il reporting.  <br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.<br/>vhlVersion) </li> <li> **Battiti cardiaci:**<br/> s:sp:hb_version) </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome report:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.vhlVersion) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.vhlVersion) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.vhlVersion </li> </ul> |

## Metadati media in streaming standard {#standard-audio-and-video-metadata}

### Mostra le informazioni

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> MOSTRA </li> <li> **Chiave API:**<br/> media.show </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> &quot;Famiglia moderna&quot; &quot;L&#39;ultima danza&quot; &quot;Ragazza nuova&quot; </li> <li> **Descrizione:**<br/> Nome programma/serie <br/>Il nome del programma è richiesto solo se la visualizzazione fa parte di una serie.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.show) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.show) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Mostra </li> <li> **Dati contestuali:**<br/> (a.media.show) </li> <li> **Feed dati:**<br/> video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.show) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name </li> </ul> |

### Formato flusso

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> STREAM_FORMAT </li> <li> **Chiave API:**<br/> media.streamFormat </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> &quot;HD&quot; </li> <li> **Descrizione:**<br/> Formato del flusso (HD, SD)  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.format) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.format) </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome report:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.format) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.format) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.streamFormat </li> </ul> |

### Stagione

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> STAGIONE </li> <li> **Chiave API:**<br/> media.sample </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> &quot;2&quot; </li> <li> **Descrizione:**<br/> Il numero di stagione a cui appartiene lo spettacolo.  La Serie di Stagioni è necessaria solo se lo show fa parte di una serie.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.stagione) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.stagione) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Stagione </li> <li> **Dati contestuali:**<br/> (a.media.stagione) </li> <li> **Feed dati:**<br/> videoconferenza </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.stagione) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number </li> </ul> |

### Episodio

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> EPISODIO </li> <li> **Chiave API:**<br/> media.episode </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> &quot;13&quot; </li> <li> **Descrizione:**<br/> Numero dell&#39;episodio.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.episode) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.episode) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Episodio </li> <li> **Dati contestuali:**<br/> (a.media.episode) </li> <li> **Feed dati:**<br/> video episodio </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.episode) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number </li> </ul> |

### ID risorsa

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> ASSET_ID </li> <li> **Chiave API:**<br/> media.assetId </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> &quot;89745363&quot; </li> <li> **Descrizione:**<br/> Identificatore univoco per il contenuto della risorsa multimediale, ad esempio l&#39;identificatore episodio della serie TV, l&#39;identificatore della risorsa filmato o l&#39;identificatore evento live. In genere questi ID sono derivati da autorità di metadati come EIDR, TMS/Gracenote o Rovi. Questi identificatori possono anche provenire da altri sistemi proprietari o interni.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.asset) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.asset) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome report:**<br/> ID risorsa </li> <li> **Dati contestuali:**<br/> (a.media.asset) </li> <li> **Feed dati:**<br/> video.videoclassificationassetid </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.asset) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.@id </li> </ul> |

### Genere

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> GENERE </li> <li> **Chiave API:**<br/> media.genre </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> &quot;Drama&quot;, &quot;Commedia&quot; </li> <li> **Descrizione:**<br/> Tipo o raggruppamento di contenuti definiti dal produttore del contenuto. I valori devono essere delimitati da virgole nell’implementazione delle variabili. Nel reporting, l’eVar elenco suddivide ogni valore in una riga, con ogni riga che riceve lo stesso peso delle metriche.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.genre) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.genre) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar elenco </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Genere </li> <li> **Dati contestuali:**<br/> (a.media.genre) </li> <li> **Feed dati:**<br/> videogame </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.genre) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre </li> </ul> |

### Data del primo volo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> FIRST_AIR_DATE </li> <li> **Chiave API:**<br/> media.firstAirDate </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> &quot;2016-01-25&quot; </li> <li> **Descrizione:**<br/> La data in cui il contenuto è andato in onda per la prima volta in televisione. Qualsiasi formato di data è accettabile, ma l’Adobe consiglia: AAAA-MM-GG </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.airDate) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.airDate) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Data del primo volo </li> <li> **Dati contestuali:**<br/> (a.media.airDate) </li> <li> **Feed dati:**<br/> video.video.videoclassificationairdate </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.airDate) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.firstAirDate </li> </ul> |

### Prima data digitale

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> FIRST_DIGITAL_DATE </li> <li> **Chiave API:**<br/> media.firstDigitalDate </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> &quot;2016-01-25&quot; </li> <li> **Descrizione:**<br/> La data in cui il contenuto è stato trasmesso per la prima volta su qualsiasi canale o piattaforma digitale. Qualsiasi formato di data è accettabile, ma l’Adobe consiglia: AAAA-MM-GG </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.digitalDate) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.digitalDate) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome report:**<br/> Prima data digitale </li> <li> **Dati contestuali:**<br/> (a.media.digitalDate) </li> <li> **Feed dati:**<br/> video.video.videoclassificationdigitaldate </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.digitalDate) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.xmpDM:releaseDate </li> </ul> |

### Valutazione dei contenuti

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> RATING </li> <li> **Chiave API:**<br/> media.rating </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> TVG, TVG, TVPG, TVMA </li> <li> **Descrizione:**<br/> Classificazione come definita dalle linee guida per i genitori dei televisori.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.rating) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.rating) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome report:**<br/> Valutazione dei contenuti </li> <li> **Dati contestuali:**<br/> (a.media.rating) </li> <li> **Feed dati:**<br/> video.videoclassificazioni </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.rating) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue </li> </ul> |

### Originatore

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> ORIGINATORE </li> <li> **Chiave API:**<br/> media.originator </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> &quot;Warner Brothers&quot;, &quot;Sony&quot;, &quot;Disney&quot; </li> <li> **Descrizione:**<br/> Creatore del contenuto.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.originator) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.originator) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> Classificazione </li> <li> **Nome report:**<br/> Originatore </li> <li> **Dati contestuali:**<br/> (a.media.originator) </li> <li> **Feed dati:**<br/> video.videoclassificazioni originator </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.originator) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name </li> </ul> |

### Rete 

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> RETE </li> <li> **Chiave API:**<br/> media.network </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> &quot;Fox&quot;, &quot;Bravo&quot;, &quot;ESPN&quot; </li> <li> **Descrizione:**<br/> Nome di rete/canale.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.network) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.network) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Rete </li> <li> **Dati contestuali:**<br/> (a.media.network) </li> <li> **Feed dati:**<br/> videonetwork </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.network) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.broadcastNetwork </li> </ul> |

### Mostra tipo

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> SHOW_TYPE </li> <li> **Chiave API:**<br/> media.showType </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> &quot;0&quot; = episodio completo; &quot;1&quot; = Anteprima/trailer; &quot;2&quot; = Clip; &quot;3&quot; = altro. </li> <li> **Descrizione:**<br/> Tipo di contenuto, espresso come numero intero compreso tra 0 e 3.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.type) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.type) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Mostra tipo </li> <li> **Dati contestuali:**<br/> (a.media.type) </li> <li> **Feed dati:**<br/> videoshowtype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.type) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.showType </li> </ul> |

### MVPD

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> MVPD </li> <li> **Chiave API:**<br/> media.pass.mvpd </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> &quot;Comcast&quot;, &quot;DirectTV&quot;, &quot;Dish&quot; </li> <li> **Descrizione:**<br/> MVPD fornito tramite autenticazione Adobe.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.pass.mvpd) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.pass.<br/>mvpd) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> MVPD </li> <li> **Dati contestuali:**<br/> (a.media.pass.mvpd) </li> <li> **Feed dati:**<br/> videomvpd </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pass.mvpd) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.idp </li> </ul> |

### Autorizzato

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> AUTORIZZATO </li> <li> **Chiave API:**<br/> media.pass.auth </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> &quot;TRUE&quot; </li> <li> **Descrizione:**<br/> L’utente è stato autorizzato tramite autenticazione Adobe.  <br/>**Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.pass.auth) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.pass.<br/>auth) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Autorizzato </li> <li> **Dati contestuali:**<br/> (a.media.pass.auth) </li> <li> **Feed dati:**<br/> videoautorizzato </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pass.auth) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.mediaAuth </li> </ul> |

### Parte giorno

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> DAY_PART </li> <li> **Chiave API:**<br/> media.dayPart </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> </li> <li> **Descrizione:**<br/> Proprietà che definisce l’ora del giorno in cui il contenuto è stato trasmesso o riprodotto. Questo potrebbe avere qualsiasi valore impostato come necessario dai clienti.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.dayPart) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.dayPart) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Parte giorno </li> <li> **Dati contestuali:**<br/> (a.media.dayPart) </li> <li> **Feed dati:**<br/> videodaypart </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.dayPart) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.dayPart </li> </ul> |

### Tipo di feed multimediale

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> FEED </li> <li> **Chiave API:**<br/> media.feed </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 </li> <li> **Valore di esempio:**<br/> &quot;East-HD&quot;, &quot;West-HD&quot;, &quot;East-SD&quot; </li> <li> **Descrizione:**<br/> Tipo di feed.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.feed) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.feed) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Tipo di feed multimediale </li> <li> **Dati contestuali:**<br/> (a.media.feed) </li> <li> **Feed dati:**<br/> videofeedtype </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.feed) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.sourceFeed </li> </ul> |

### Artista

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.artist </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 <br/>Disponibile in [Panoramica della raccolta multimediale](/help/media-collection-api/mc-api-overview.md) o [Download degli SDK - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> &quot;I Beatles&quot; </li> <li> **Descrizione:**<br/> Nome dell&#39;artista.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.artist) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.artista) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Artista</li> <li> **Dati contestuali:**<br/> (a.media.artist) </li> <li> **Feed dati:**<br/> videoaudioartista </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.artista) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.Audio.xmpDM:artista </li> </ul> |

### Album

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.album </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 <br/>Disponibile in [Panoramica della raccolta multimediale](/help/media-collection-api/mc-api-overview.md) o [Download degli SDK - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> &quot;Revolver&quot; </li> <li> **Descrizione:**<br/> Nome dell&#39;album.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.album) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.album) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Album </li> <li> **Dati contestuali:**<br/> (a.media.album) </li> <li> **Feed dati:**<br/> videoaudioalbum </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.album) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.Audio.xmpDM:album </li> </ul> |

### Etichetta

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.label </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 <br/>Disponibile in [Panoramica della raccolta multimediale](/help/media-collection-api/mc-api-overview.md) o [Download degli SDK - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> &quot;Revolver&quot; </li> <li> **Descrizione:**<br/> Nome dell&#39;etichetta del record.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.label) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.label) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Etichetta</li> <li> **Dati contestuali:**<br/> (a.media.label) </li> <li> **Feed dati:**<br/> videoaudiolibro </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.label) </li> <li> **Percorso campo XDM:**<br/>  </li> </ul> |

### Autore

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.author </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 <br/>Disponibile in [Panoramica della raccolta multimediale](/help/media-collection-api/mc-api-overview.md) o [Download degli SDK - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> &quot;John Kennedy Toole&quot; </li> <li> **Descrizione:**<br/> Nome dell’autore (di un audiolibro).  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.author) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.author) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Autore </li> <li> **Dati contestuali:**<br/> (a.media.author) </li> <li> **Feed dati:**<br/> videoaudioautore </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.author) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference.Audio.dc:creator </li> </ul> |

### Stazione

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.station </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 <br/>Disponibile in [Panoramica della raccolta multimediale](/help/media-collection-api/mc-api-overview.md) o [Download degli SDK - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> &quot;NPR&quot; </li> <li> **Descrizione:**<br/> Nome/ID della stazione radio.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.station) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.station) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Stazione </li> <li> **Dati contestuali:**<br/> (a.media.station) </li> <li> **Feed dati:**<br/> videoconferenza </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.station) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference._id3.audio._id3.TRSN </li> </ul> |

### Editore

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> </li> <li> **Chiave API:**<br/> media.publisher </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Media Start, chiusura file multimediali </li> <li> **Min Versione SDK:** 1,5,7 <br/>Disponibile in [Panoramica della raccolta multimediale](/help/media-collection-api/mc-api-overview.md) o [Download degli SDK - Versioni 2.2](/help/sdk-implement/download-sdks.md).  </li> <li> **Valore di esempio:**<br/> &quot;Random Bauhaus&quot; </li> <li> **Descrizione:**<br/> Nome dell’autore del contenuto audio.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.publisher) </li> <li> **Battiti cardiaci:**<br/> s:meta:<br/>a.media.publisher) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> HIT </li> <li> **Nome report:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.publisher) </li> <li> **Feed dati:**<br/> videoaudiopublisher </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.publisher) </li>  <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetReference._id3.audio._id3.TPUB </li> </ul> |

## Metriche per contenuti multimediali in streaming {#audio-and-video-metrics}

### Media Starts

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente</li> <li> **Chiave API:**<br/> N/D</li> <li> **Tipo:**<br/> string</li> <li> **Inviato con:**<br/> Media Start</li> <li> **Min Versione SDK:** Qualsiasi</li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Evento Load per il contenuto multimediale. (Questo si verifica quando il visualizzatore fa clic sul pulsante _Play_ ). Questo vale anche se ci sono annunci pre-roll, buffering, errori e così via.  <br/>**Importante:**  Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (a.media.view) </li> <li> **Battiti cardiaci:**<br/> s:event:<br/>type=start) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Media Starts </li> <li> **Dati contestuali:**<br/> (a.media.view) </li> <li> **Feed dati:**<br/> videostart </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.view) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.started.value, media.mediaTimed.dropBeforeStart.value </li> </ul> |

### Inizio contenuti

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Viene utilizzato il primo fotogramma del file multimediale. Se l’utente cade durante l’annuncio, il buffering, ecc., non ci sarebbe alcun evento &quot;Inizio contenuto&quot;.  <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Inizio contenuti </li> <li> **Dati contestuali:**<br/> (a.media.play) </li> <li> **Feed dati:**<br/> video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.play) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.dropBeforeStart.value </li> </ul> |

### Contenuto completato {#content-complete}

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Un ruscello che è stato guardato al completamento. Ciò non significa necessariamente che l&#39;utente abbia guardato o ascoltato l&#39;intero flusso; avrebbero potuto saltare in avanti. Questo significa solo che l’utente ha raggiunto la fine del flusso, il 100%. <br/>Vedi anche [Fine sessione](quality-parameters.md#session-end) <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> s:event:<br/>type=complete) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Completamento contenuto </li> <li> **Dati contestuali:**<br/> (a.media.complete) </li> <li> **Feed dati:**<br/> video   </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.complete) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.complete.value </li> </ul> |

### Tempo contenuto trascorso

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 105 </li> <li> **Descrizione:**<br/> Riepiloga la durata dell’evento (in secondi) per tutti gli eventi di tipo PLAY sul contenuto principale.  Il valore viene visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Tempo contenuto trascorso </li> <li> **Dati contestuali:**<br/> (a.media.timePlayed) </li> <li> **Feed dati:**<br/> tempo video </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.timePlayed) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.dropBeforeStart.value </li> </ul> |

### Tempo trascorso per contenuti multimediali

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 120 </li> <li> **Descrizione:**<br/> Riassume la durata dell’evento (in secondi) per tutti gli eventi di tipo PLAY, sia principali che di tipo annuncio.  Il valore viene visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Tempo trascorso per contenuti multimediali </li> <li> **Dati contestuali:**<br/> (a.media.totalTimePlayed) </li> <li> **Feed dati:**<br/> videototaltime </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.totalTimePlayed) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.totalTimePlayed.value </li> </ul> |

### Tempo unico riprodotto

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 94 </li> <li> **Descrizione:**<br/> Il valore in secondi dei segmenti univoci di contenuto riprodotti durante una sessione. Esclude il tempo di riproduzione in scenari di ricerca indietro in cui un visualizzatore sta guardando lo stesso segmento del contenuto più volte.  Il valore viene visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi.  <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Tempo unico riprodotto </li> <li> **Dati contestuali:**<br/> (a.media.uniqueTimePlayed) </li> <li> **Feed dati:**<br/> videouniquetimeplay </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.uniqueTimePlayed) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.uniqueTimePlayed.value </li> </ul> |

### Marcatore progresso 10 %

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> La testina di riproduzione passa il marcatore del 10% del contenuto in base alla lunghezza. Il marcatore viene conteggiato una sola volta, anche se cerca all’indietro. Se si cerca in avanti, i marcatori saltati non vengono conteggiati.  <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Marcatore progresso 10% </li> <li> **Dati contestuali:**<br/> (a.media.progress10) </li> <li> **Feed dati:**<br/> video-progress10 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress10) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.progress10.value </li> </ul> |

### Marcatore progresso 25 %

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> La testina di riproduzione passa il marcatore del 25% del contenuto in base alla lunghezza del contenuto. Il marcatore conteggia una sola volta, anche se cerca all’indietro. Se si cerca in avanti, i marcatori saltati non vengono conteggiati.  <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Marcatore progresso 25% </li> <li> **Dati contestuali:**<br/> (a.media.progress25) </li> <li> **Feed dati:**<br/> video-progress25 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress25) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.progress25.value </li> </ul> |

### Marcatore progresso 50 %

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> La testina di riproduzione passa il marcatore del 50% del contenuto in base alla lunghezza del contenuto. Il marcatore conteggia una sola volta, anche se cerca all’indietro. Se si cerca in avanti, i marcatori saltati non vengono conteggiati.  <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Marcatore progresso 50% </li> <li> **Dati contestuali:**<br/> (a.media.progress50) </li> <li> **Feed dati:**<br/> video-progress50 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress50) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.progress50.value </li> </ul> |

### Marcatore progresso 75 %

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> **N/D** </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> La testina di riproduzione passa il marcatore del 75% del contenuto in base alla lunghezza del contenuto. Il marcatore conteggia una sola volta, anche se cerca all’indietro. Se si cerca in avanti, i marcatori saltati non vengono conteggiati.  <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Marcatore progresso 75% </li> <li> **Dati contestuali:**<br/> (a.media.progress75) </li> <li> **Feed dati:**<br/> video progress75 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress75) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.progress75.value </li> </ul> |

### Marcatore progresso 95 %

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> La testina di riproduzione passa il marcatore del 95% del contenuto in base alla lunghezza del contenuto. Il marcatore conteggia una sola volta, anche se cerca all’indietro. Se si cerca in avanti, i marcatori saltati non vengono conteggiati.  <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Marcatore progresso 95% </li> <li> **Dati contestuali:**<br/> (a.media.progress95) </li> <li> **Feed dati:**<br/> video progress95 </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.progress95) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.progress95.value </li> </ul> |

### Pubblico medio per minuto

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> Maggiore o uguale a 1 </li> <li> **Descrizione:**<br/> La metrica Media Minute Audience viene calcolata come Tempo totale di contenuto trascorso, per un elemento multimediale specifico, diviso per la sua lunghezza per tutte le sessioni di riproduzione: <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Pubblico medio per minuto </li> <li> **Dati contestuali:**<br/> (a.media.averageMinuteAudience) </li> <li> **Feed dati:**<br/> videoaverageminuteaudience </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.averageMinuteAudience) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.averageMinuteAudience.value </li> </ul> |

### Secondi dall’ultima chiamata

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 600</li> <li> **Descrizione:**<br/> La metrica secondi dall’ultima chiamata è 0 se il flusso è stato chiuso con un evento completo o con un evento finale e in genere è 600 se è stato chiuso a causa del timeout. Questa metrica non dispone di una variabile di soluzione e di regole di elaborazione automatica, pertanto devi creare una regola di elaborazione personalizzata per salvarla.</li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome report:**<br/> Personalizzato</li> <li> **Dati contestuali:**<br/> (a.media.secondsSinceLastCall) </li> <li> **Feed dati:**<br/> videoseconssincelastic </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.secondsSinceLastCall) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.primaryAssetViewDetails.sessionTimeout </li> </ul> |

### Dati federati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> booleano </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> true  </li> <li> **Descrizione:**<br/> Imposta su true quando l&#39;hit viene federato (ovvero, ricevuto dal cliente come parte di una condivisione di dati federata, anziché come implementazione). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome report:**<br/> N/D </li> <li> **Dati contestuali:**<br/> (a.media.federated) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.federated) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.federated.value </li> </ul> |

### Flussi stimati

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 1 - per una riproduzione di 19 minuti; <br/>2 - per 31 minuti di riproduzione; <br/>3 - Per una riproduzione di 78 minuti. </li> <li> **Descrizione:**<br/> Numero stimato di flussi video o audio per ogni singolo contenuto. Questo valore viene aumentato per ogni 30 minuti di tempo di riproduzione (contenuto + annunci). I clienti devono creare le proprie regole di elaborazione per disporre del valore disponibile per il reporting. <br/><br/>Un flusso viene conteggiato ogni 30 minuti, in base al `ms_s` (o totalTimePlayed = Video Total Time), simile a: <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome report:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.EstimatedStreams) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.EstimStreams) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.EstimatedStreams.value </li> </ul> |

### Flussi interessati in pausa

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** 1.5.6 </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Questo valore è vero o falso. È vero se si sono verificate una o più pause durante la riproduzione di un singolo elemento multimediale.  <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Flusso in pausa </li> <li> **Dati contestuali:**<br/> (a.media.pause) </li> <li> **Feed dati:**<br/> videopausa </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pause) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.pauseImpactedStreams.value > 0 => &quot;TRUE&quot; </li> </ul> |

### Pausa eventi

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** 1.5.6 </li> <li> **Valore di esempio:**<br/> 2 </li> <li> **Descrizione:**<br/> Questa metrica viene calcolata come un conteggio dei periodi di pausa che si sono verificati durante una sessione di riproduzione.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> s:event:<br/>type=pause) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Pausa eventi </li> <li> **Dati contestuali:**<br/> (a.media.pauseCount) </li> <li> **Feed dati:**<br/> videopausecount </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pauseCount) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.pauses.value </li> </ul> |

### Durata totale pausa

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** 1.5.6 </li> <li> **Valore di esempio:**<br/> 190 </li> <li> **Descrizione:**<br/> Somma la durata (in secondi) di tutti gli eventi di tipo PAUSE. Il valore viene visualizzato nel formato ora (HH:MM:SS) in Analysis Workspace e Reports &amp; Analytics. In Feed dati, Data Warehouse e API di reporting i valori verranno visualizzati in secondi. <br/> **Data di rilascio: 13/09/18** </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Durata totale pausa </li> <li> **Dati contestuali:**<br/> (a.media.pauseTime) </li> <li> **Feed dati:**<br/> (videopausetime) </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.pauseTime) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.pauseTime.value </li> </ul> |

### Riprende il contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> **media.curriculum** </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** 1.5.6 </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Viene conteggiato un Riprendi per ogni riproduzione che riprende dopo più di 30 minuti di buffer, pausa o periodo di arresto OPPURE se questo valore viene impostato dal lettore sul trackPlay VideoInfo. <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore.  </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> s:event:<br/>type=curriculum) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Riprende il contenuto </li> <li> **Dati contestuali:**<br/> (a.media.curriculum) </li> <li> **Feed dati:**<br/> videoresume </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.curriculum) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.currices.value > 0 => &quot;TRUE&quot; </li> </ul> |

### Visualizzazioni dei segmenti di contenuto

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> Imposta automaticamente </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> string </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> TRUE </li> <li> **Descrizione:**<br/> Numero di visualizzazioni del contenuto principale. Viene conteggiata una visualizzazione segmento di contenuto quando viene visualizzato almeno un fotogramma.  <br/> **Importante:** Questo può essere vero solo se è impostato. Se non è impostato, non viene restituito alcun valore. </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> event </li> <li> **Nome report:**<br/> Visualizzazioni dei segmenti di contenuto </li> <li> **Dati contestuali:**<br/> (a.media.segmentView) </li> <li> **Feed dati:**<br/> video segmentevisualizzazioni </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.segmentView) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.mediaSegmentViews.value > 0 => &quot;TRUE&quot; </li> </ul> |


### Conteggio annunci

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> N/D </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 2 </li> <li> **Descrizione:**<br/> Il numero di annunci avviati durante la sessione multimediale.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome report:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.adCount) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.adCount) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.adCount.value </li> </ul> |

### Conteggio capitoli

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> N/D </li> <li> **Chiave API:**<br/> N/D </li> <li> **Tipo:**<br/> numero </li> <li> **Inviato con:**<br/> Chiudi file multimediali </li> <li> **Min Versione SDK:** Qualsiasi </li> <li> **Valore di esempio:**<br/> 2 </li> <li> **Descrizione:**<br/> Il numero di capitoli avviati durante la sessione multimediale.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/D </li> <li> **Battiti cardiaci:**<br/> N/D </li> </ul> | <ul> <li> **Disponibile:**<br/> Usa regola di elaborazione personalizzata </li> <li> **Variabile riservata:**<br/> N/D </li> <li> **Nome report:**<br/> Personalizzato </li> <li> **Dati contestuali:**<br/> (a.media.capitoloCount) </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.capitoloCount) </li> <li> **Percorso campo XDM:**<br/> media.mediaTimed.capitoloCount.value </li> </ul> |


## Parametri del California Consumer Privacy Act (CCPA) {#ccpa-params}

### Inoltro lato server di rinuncia

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> N/D </li> <li> **Chiave API:**<br/> analytics.optOutServerSideForwarding </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> booleano </li> <li> **Inviato con:**<br/> Media Start </li> <li> **Min Versione SDK:** N/D </li> <li> **Valore di esempio:**<br/> true </li> <li>**Descrizione:**<br/> Imposta su true quando l’utente finale ha rinunciato alla condivisione dei propri dati tra Adobe Analytics e altre soluzioni di Experience Cloud (ad Audience Manager). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (opt.dmp) </li> <li> **Battiti cardiaci:**<br/> s:meta:cm.ssf) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> In visita </li> <li> **Nome report:**<br/> N/D </li> <li> **Dati contestuali:**<br/> N/D </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> N/D </li> <li> **Percorso campo XDM:**<br/>  </li> </ul> |

### Consenso negato

|   Implementazione   | Parametri di rete | Generazione di rapporti |
| --- | --- | --- |
| <ul> <li> **Chiave SDK:**<br/> N/D </li> <li> **Chiave API:**<br/> analytics.optOutShare </li> <li> **Obbligatorio:**<br/> No </li> <li> **Tipo:**<br/> booleano </li> <li> **Inviato con:**<br/> Media Start </li> <li> **Min Versione SDK:** N/D </li> <li> **Valore di esempio:**<br/> true </li> <li>**Descrizione:**<br/> Impostato su true quando l’utente finale ha rinunciato alla federazione dei propri dati (ad esempio ad altri client Adobe Analytics). </li></ul> | <ul> <li> **Adobe Analytics:**<br/> (opt.oos) </li> <li> **Battiti cardiaci:**<br/> s:meta:cm.oos) </li> </ul> | <ul> <li> **Disponibile:**<br/> Sì </li> <li> **Variabile riservata:**<br/> eVar </li> <li> **Scadenza:**<br/> In visita </li> <li> **Nome report:**<br/> N/D </li> <li> **Dati contestuali:**<br/> N/D </li> <li> **Feed dati:**<br/> N/D </li> <li> **Audience Manager:**<br/> N/D </li> <li> **Percorso campo XDM:**<br/>  </li> </ul> |

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
