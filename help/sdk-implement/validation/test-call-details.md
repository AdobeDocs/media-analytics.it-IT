---
seo-title: Test dei dettagli della chiamata
title: Test dei dettagli della chiamata
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
translation-type: tm+mt
source-git-commit: d694ced982140c1f8020c0be304492aee0495cdc

---


# Test dei dettagli della chiamata{#test-call-details}

## Avviare il lettore multimediale {#start-the-media-player}

### Chiamata di avvio di Adobe Analytics (AppMeasurement) {#aa-start-call}

| Parametro |  Valore (esempio) |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Titolo episodio |
| _**`a.media.name`**_ | _**123456**_ |
| _**`a.media.length`**_ | _**120**_ |
| `a.media.playerName` | HTML5 |
| _**`a.media.view`**_ | _**true**_ |
| `a.contentType` | vod |
| _**`custom.[value]`**_ | _**Campi di metadati personalizzati**_ |
| _**`a.media.[value]`**_ | _**Campi metadati standard**_ |

**Note:**

* Devono essere presenti ulteriori variabili di dati di contesto contenenti metadati. Consultate i dettagli dei metadati di seguito.
* La lunghezza dei flussi lineari deve essere impostata sulla migliore stima per la presentazione corrente.

### Metadati standard nella chiamata di avvio di Adobe Analytics (AppMeasurement) {#std-metadata-aa}

| Parametro |  Valore (esempio) |
|---|---|
| `a.media.show` | Mostra titolo |
| `a.media.season` | 6 |
| `a.media.episode` | Titolo episodio |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | commedia |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | casa di produzione |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | sbloccato |
| `a.media.feed` | nessun feed |
| `a.media.stream_format` | 0 |

### Metadati personalizzati nella chiamata di avvio di Adobe Analytics (AppMeasurement) {#custom-metadata-aa}

| Parametro |  Valore (esempio) |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

### Avvio della chiamata di Media Analytics (heartbeat) {#ma-start-call}

| Parametro |  Valore (esempio) |
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
| _**`s:meta:a.media.[value]`**_ | _**Campi metadati standard**_ |

**Note:**

* Devono essere presenti ulteriori variabili di dati di contesto contenenti metadati. Consultate i dettagli dei metadati di seguito.
* La posizione dell'indicatore di riproduzione per i flussi lineari all'avvio del video deve essere impostata sui secondi trascorsi dall'inizio della presentazione corrente, non su 0.

### Metadati standard nella chiamata di avvio di Media Analytics (heartbeat) {#std-metadata-ma}

| Parametro |  Valore (esempio) |
|---|---|
| `s:meta:a.media.show` | Mostra le informazioni |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Titolo episodio |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | commedia |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | casa di produzione |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | sbloccato |
| `s:meta:a.media.feed` | nessun feed |
| `s:meta:a.media.stream_format` | 0 |

### Metadati personalizzati nella chiamata di avvio di Media Analytics (heartbeat) {#custom-metadata-ma}

| Parametro |  Valore (esempio) |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Guida introduttiva ad Adobe Analytics (heartbeat) {#ma-aa-start}

| Parametro |  Valore (esempio) |
|---|---|
| _**`s:event:type`**_ | _**a_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Titolo episodio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Note:**

* Questa chiamata indica che Media SDK ha richiesto l’invio di una `pev2=ms_s` chiamata Adobe Analytics al server Adobe Analytics (AppMeasurement).
* Questa chiamata non contiene metadati personalizzati.

## Visualizzazione e riproduzione {#view-ad-playback}

### Adobe Analytics (AppMeasurement): chiamata ad avvio annuncio {#aa-ad-start-call}

| Parametro |  Valore (esempio) |
|---|---|
| _**`pev2`**_ | _**msa_s**_ |
| `a.media.name` | 123456 |
| _**`a.media.ad.name`**_ | _**9378**_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| _**`a.media.ad.length`**_ | _**15**_ |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| _**`a.media.ad.view`**_ | _**True**_ |
| _**`custom.[value]`**_ | _**Campi metadati**_ |
| _**`a.media.[value]`**_ | _**Campi metadati standard**_ |

**Note:**

* Devono essere presenti ulteriori variabili di dati di contesto contenenti metadati. Consultate i dettagli dei metadati di seguito.
* La lunghezza dell'annuncio può essere impostata su -1 se non è disponibile all'inizio dell'annuncio.

### Metadati standard in Adobe Analytics (AppMeasurement) Annuncio Start {#std-metadata-aa-ad-start}

| Parametro |  Valore (esempio) |
|---|---|
| `a.media.show` | Mostra titolo |
| `a.media.season` | 6 |
| `a.media.episode` | Titolo episodio |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | commedia |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | casa di produzione |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | sbloccato |
| `a.media.feed` | nessun feed |
| `a.media.stream_format` | 0 |

### Metadati personalizzati in Adobe Analytics (AppMeasurement) Annuncio Start {#custom-metadata-aa-ad-start}

| Parametro |  Valore (esempio) |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Media Analytics (heartbeat): chiamata Ad Start {#ma-ad-start-call}

| Parametro |  Valore (esempio) |
|---|---|
| _**`s:event:type`**_ | _**start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _**`l:asset:length`**_ | _**120**_ |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |
| _**`s:meta:custom.[value]`**_ | _**Campi di metadati personalizzati**_ |
| _**`s:meta:a.media.[value]`**_ | _**Campi metadati standard**_ |

**Note:**

* Devono essere presenti ulteriori variabili di dati di contesto contenenti metadati. Consultate i dettagli dei metadati di seguito.
* La lunghezza dell'annuncio può essere impostata su -1 se non è disponibile all'inizio dell'annuncio.

### Metadati standard in Media Analytics (heartbeat) Chiamata Ad Start {#std-metadata-ma-ad-start}

| Parametro |  Valore (esempio) |
|---|---|
| `s:meta:a.media.show` | Mostra le informazioni |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Titolo episodio |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | commedia |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | casa di produzione |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | sbloccato |
| `s:meta:a.media.feed` | nessun feed |
| `s:meta:a.media.stream_format` | 0 |

### Metadati personalizzati in Media Analytics (heartbeat): chiamata Ad Start {#custom-metadata-ma-ad-start}

| Parametro |  Valore (esempio) |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics (heartbeat): chiamata Adobe Analytics Ad Start {#ma-aa-ad-start-call}

| Parametro |  Valore (esempio) |
|---|---|
| _**`s:event:type`**_ | _**aa_ad_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Chiamata ad Analytics Media (heartbeat) {#ma-ad-play-call}

| Parametro |  Valore (esempio) |
|---|---|
| _**`s:event:type`**_ | _**play**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Analisi dei supporti (heartbeat) Chiamata Ad Pause {#ma-ad-pause-call}

| Parametro |  Valore (esempio) |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Media Analytics (heartbeat): chiamata Adobe Analytics Ad Complete {#ma-aa-ad-complete-call}

| Parametro |  Valore (esempio) |
|---|---|
| _**`s:event:type`**_ | _**complete**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

## Riproduci contenuto principale {#play-main-content}

### Media Analytics (heartbeat) Riproduci una chiamata {#ma-play-call}

| Parametro |  Valore (esempio) |
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

* La posizione dell'indicatore di riproduzione dovrebbe aumentare di 10 secondi con ogni chiamata di riproduzione.
* Il `l:event:duration` valore rappresenta il numero di millisecondi trascorsi dall’ultima chiamata di tracciamento e deve corrispondere all’incirca allo stesso valore per ogni chiamata di 10 secondi.

## Pausa del contenuto principale {#pause-main-content}

### Media Analytics (heartbeat) - Sospendi chiamata {#ma-pause-call}

| Parametro |  Valore (esempio) |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| _**`l:event:playhead`**_ | _**29**_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Titolo episodio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |


