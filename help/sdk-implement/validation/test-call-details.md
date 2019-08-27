---
seo-title: Dettagli della chiamata di test
title: Dettagli della chiamata di test
uuid: d 3 a 0 e 62 f -2 fc 3-413 d-ac 56-adbbc 9 b 3 e 983
translation-type: tm+mt
source-git-commit: d694ced982140c1f8020c0be304492aee0495cdc

---


# Dettagli della chiamata di test{#test-call-details}

## Avviare il lettore multimediale {#start-the-media-player}

### Chiamata di avvio di Adobe Analytics (appmeasurement) {#aa-start-call}

| Parametro | Valore (campione)  |
|---|---|
| `pev2` | ms_ s |
| `a.media.friendlyName` | Titolo episodio |
| _**`a.media.name`**_ | _**123456**_ |
| _**`a.media.length`**_ | _**120**_ |
| `a.media.playerName` | HTML5 |
| _**`a.media.view`**_ | _**true**_ |
| `a.contentType` | vod |
| _**`custom.[value]`**_ | _**Campi di metadati personalizzati**_ |
| _**`a.media.[value]`**_ | _**Campi di metadati standard**_ |

**Note:**

* Devono essere presenti e contenenti metadati ulteriori variabili di dati di contesto. Consultate i dettagli sui metadati di seguito.
* La lunghezza dei flussi lineari deve essere impostata sulla stima migliore per l'attuale visualizzazione.

### Metadati standard nella chiamata di avvio di Adobe Analytics (appmeasurement) {#std-metadata-aa}

| Parametro | Valore (campione)  |
|---|---|
| `a.media.show` | Mostra titolo |
| `a.media.season` | 6 |
| `a.media.episode` | Titolo episodio |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV -14 |
| `a.media.originator` | casa produzione |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlock |
| `a.media.feed` | nessun feed |
| `a.media.stream_format` | 0 |

### Metadati personalizzati nella chiamata di avvio di Adobe Analytics (appmeasurement) {#custom-metadata-aa}

| Parametro | Valore (campione)  |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

### Media Analytics (heartbeats) Chiamata di inizio {#ma-start-call}

| Parametro | Valore (campione)  |
|---|---|
| `s:event:type` | start |
| _**`l:event:playhead`**_ | _**0**_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Titolo episodio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| _**`s:meta:custom.[value]`**_ | _**Campi di metadati personalizzati**_ |
| _**`s:meta:a.media.[value]`**_ | _**Campi di metadati standard**_ |

**Note:**

* Devono essere presenti e contenenti metadati ulteriori variabili di dati di contesto. Consultate i dettagli sui metadati di seguito.
* La posizione della linea di scansione per i flussi lineari all'avvio del video deve essere impostata sui secondi trascorsi dall'inizio della visualizzazione corrente, non da 0.

### Metadati standard in Media Analytics (heartbeats) Chiamata di inizio {#std-metadata-ma}

| Parametro | Valore (campione)  |
|---|---|
| `s:meta:a.media.show` | Mostra le informazioni |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Titolo episodio |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV -14 |
| `s:meta:a.media.originator` | casa produzione |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlock |
| `s:meta:a.media.feed` | nessun feed |
| `s:meta:a.media.stream_format` | 0 |

### Metadati personalizzati in Media Analytics (heartbeats) Chiamata di inizio {#custom-metadata-ma}

| Parametro | Valore (campione)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics (heartbeats) Chiamata di avvio di Adobe Analytics {#ma-aa-start}

| Parametro | Valore (campione)  |
|---|---|
| _**`s:event:type`**_ | _**aa_ start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Titolo episodio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Note:**

* Questa chiamata indica che Media SDK ha richiesto l'invio di una `pev2=ms_s` chiamata Adobe Analytics al server di Adobe Analytics (appmeasurement).
* Questa chiamata non contiene metadati personalizzati.

## Visualizzare la riproduzione degli annunci {#view-ad-playback}

### Chiamata ad Adobe Analytics (appmeasurement) Ad Start {#aa-ad-start-call}

| Parametro | Valore (campione)  |
|---|---|
| _**`pev2`**_ | _**msa_ s**_ |
| `a.media.name` | 123456 |
| _**`a.media.ad.name`**_ | _**9378**_ |
| `a.media.ad.friendlyName` | Video_ VPAID_ DFA |
| `a.media.ad.podFriendlyName` | preroll |
| _**`a.media.ad.length`**_ | _**15**_ |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c 27 aaf 3 ff 8224 bb 6 b 9 ebfe 1 b 2 e 79073 d_ 1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| _**`a.media.ad.view`**_ | _**True**_ |
| _**`custom.[value]`**_ | _**Campi metadati**_ |
| _**`a.media.[value]`**_ | _**Campi di metadati standard**_ |

**Note:**

* Devono essere presenti e contenenti metadati ulteriori variabili di dati di contesto. Consultate i dettagli sui metadati di seguito.
* La lunghezza dell'annuncio può essere impostata su -1 se non è disponibile all'avvio.

### Metadati standard in Adobe Analytics (appmeasurement) Call Start {#std-metadata-aa-ad-start}

| Parametro | Valore (campione)  |
|---|---|
| `a.media.show` | Mostra titolo |
| `a.media.season` | 6 |
| `a.media.episode` | Titolo episodio |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV -14 |
| `a.media.originator` | casa produzione |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlock |
| `a.media.feed` | nessun feed |
| `a.media.stream_format` | 0 |

### Metadati personalizzati in Adobe Analytics (appmeasurement) Call Start {#custom-metadata-aa-ad-start}

| Parametro | Valore (campione)  |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Media Analytics (heartbeats) Chiamata Ad Avvio {#ma-ad-start-call}

| Parametro | Valore (campione)  |
|---|---|
| _**`s:event:type`**_ | _**start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _**`l:asset:length`**_ | _**120**_ |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |
| _**`s:meta:custom.[value]`**_ | _**Campi di metadati personalizzati**_ |
| _**`s:meta:a.media.[value]`**_ | _**Campi di metadati standard**_ |

**Note:**

* Devono essere presenti e contenenti metadati ulteriori variabili di dati di contesto. Consultate i dettagli sui metadati di seguito.
* La lunghezza dell'annuncio può essere impostata su -1 se non è disponibile all'avvio.

### Metadati standard in Media Analytics (heartbeats) Chiamata Ad Avvio {#std-metadata-ma-ad-start}

| Parametro | Valore (campione)  |
|---|---|
| `s:meta:a.media.show` | Mostra le informazioni |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Titolo episodio |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV -14 |
| `s:meta:a.media.originator` | casa produzione |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlock |
| `s:meta:a.media.feed` | nessun feed |
| `s:meta:a.media.stream_format` | 0 |

### Metadati personalizzati in Media Analytics (heartbeats) Chiamata Ad Avvio {#custom-metadata-ma-ad-start}

| Parametro | Valore (campione)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics (heartbeats) Chiamata di Adobe Analytics Ad Start {#ma-aa-ad-start-call}

| Parametro | Valore (campione)  |
|---|---|
| _**`s:event:type`**_ | _**aa_ ad_ start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Call Analytics (heartbeats) Call Play {#ma-ad-play-call}

| Parametro | Valore (campione)  |
|---|---|
| _**`s:event:type`**_ | _**play**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Chiamata Media Analytics (heartbeats) Ad Pause call {#ma-ad-pause-call}

| Parametro | Valore (campione)  |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Media Analytics (heartbeats) Chiamata ad Adobe Analytics Ad Complete {#ma-aa-ad-complete-call}

| Parametro | Valore (campione)  |
|---|---|
| _**`s:event:type`**_ | _**complete**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

## Riproduci contenuto principale {#play-main-content}

### Chiamata di Media Analytics (heartbeats) Play {#ma-play-call}

| Parametro | Valore (campione)  |
|---|---|
| `s:event:type` | play |
| _**`l:event:playhead`**_ | _**29**_ |
| _**`l:event:duration`**_ | _**10189**_ |
| `s:asset:name` | Titolo episodio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Note:**

* La posizione dell'indicatore di riproduzione deve essere incrementata di 10 secondi con ogni chiamata di riproduzione.
* Il `l:event:duration` valore rappresenta il numero di millisecondi trascorsi dall'ultima chiamata di tracciamento e dovrebbe essere circa lo stesso valore per ogni chiamata di 10 secondi.

## Mettere in pausa il contenuto principale {#pause-main-content}

### Media Analytics (heartbeats) Pausa chiamata {#ma-pause-call}

| Parametro | Valore (campione)  |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| _**`l:event:playhead`**_ | _**29**_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Titolo episodio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |


