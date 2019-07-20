---
seo-title: Dettagli della chiamata di test
title: Dettagli della chiamata di test
uuid: d 3 a 0 e 62 f -2 fc 3-413 d-ac 56-adbbc 9 b 3 e 983
translation-type: tm+mt
source-git-commit: 400c7ada4ab269017c3c2948c9056b4c1031d793

---


# Test call details{#test-call-details}

## Start the video player {#section_qts_xff_f2b}

### Chiamata start di Media Analytics

| Parametro | Valore (esempio)  |
|---|---|
| `pev2` | ms_ s |
| `a.media.friendlyName` | Titolo episodio |
| `a.media.name` | 123456 |
| `a.media.length` | 120 |
| `a.media.playerName` | HTML5 |
| `a.media.view` | true |
| `a.contentType` | vod |
| `custom.[value]` | Campi di metadati personalizzati |
| `a.media.[value]` | Campi di metadati standard |

**Note:**

* Devono essere presenti e contenenti metadati ulteriori variabili di dati di contesto. Consultate i dettagli sui metadati di seguito.
* La lunghezza dei flussi lineari deve essere impostata sulla stima migliore per l'attuale visualizzazione.

### Metadati standard nella chiamata di avvio di Media Analytics

| Parametro | Valore (esempio)  |
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

### Chiamata di avvio heartbeat

| Parametro | Valore (esempio)  |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `l:asset:name` | Titolo episodio |
| `l:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `l:stream:type` | vod |
| `s:asset:type` | main |
| `s:meta:custom.[value]` | Campi di metadati personalizzati |
| `s:meta:a.media.[value]` | Campi di metadati standard |

### Metadati video nella chiamata di avvio di Media Analytics

| Parametro | Valore (esempio)  |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

**Note:**

* Devono essere presenti e contenenti metadati ulteriori variabili di dati di contesto. Consultate i dettagli sui metadati di seguito.
* La posizione della linea di scansione per i flussi lineari all'avvio del video deve essere impostata sui secondi trascorsi dall'inizio della visualizzazione corrente, non da 0.

### Chiamata di avvio Heartbeat Analytics

| Parametro | Valore (esempio)  |
|---|---|
| `s:event:type` | aa_ start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `l:asset:name` | Titolo episodio |
| `l:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `l:stream:type` | vod |
| `s:asset:type` | main |

### Metadati video nella chiamata di avvio Heartbeat

| Parametro | Valore (esempio)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Metadati standard nella chiamata di avvio Heartbeat

| Parametro | Valore (esempio)  |
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

**Note:**

* Questa chiamata indica che la libreria heartbeat ha richiesto che una chiamata di analisi 2 = ms_ s venga inviata al server di analisi.
* Questa chiamata non contiene metadati personalizzati.

## View ad playback {#section_wz3_yff_f2b}

### Chiamata Avvio annunci di Media Analytics

| Parametro | Valore (esempio)  |
|---|---|
| `pev2` | msa_ s |
| `a.media.name` | 123456 |
| `a.media.ad.name` | 9378 |
| `a.media.ad.friendlyName` | Video_ VPAID_ DFA |
| `a.media.ad.podFriendlyName` | preroll |
| `a.media.ad.length` | 15 |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c 27 aaf 3 ff 8224 bb 6 b 9 ebfe 1 b 2 e 79073 d_ 1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| `a.media.ad.view` | True |
| `custom.[value]` | Campi metadati |
| `a.media.[value]` | Campi di metadati standard |

**Nota:** Devono essere presenti e contenenti metadati ulteriori variabili di dati di contesto. Consultate i dettagli sui metadati di seguito.

### Chiamata avvio heartbeat

| Parametro | Valore (esempio)  |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `l:asset:ad_id` | 9378 |
| `l:asset:length` | 120 |
| `l:stream:type` | vod |
| `s:asset:type` | ad |
| `s:meta:custom.[value]` | Campi di metadati personalizzati |
| `s:meta:a.media.[value]` | Campi di metadati standard |

### Metadati video nella chiamata introduttiva ad Analytics

| Parametro | Valore (esempio)  |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Metadati standard nella chiamata di avvio annunci di Media Analytics

| Parametro | Valore (esempio)  |
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

**Note:**

* Devono essere presenti e contenenti metadati ulteriori variabili di dati di contesto. Consultate i dettagli sui metadati di seguito.
* La lunghezza dell'annuncio può essere impostata su -1 se non è disponibile all'avvio.

### Chiamata introduttiva ad Analytics Analytics

| Parametro | Valore (esempio)  |
|---|---|
| `s:event:type` | aa_ ad_ start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `l:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `l:stream:type` | vod |
| `s:asset:type` | ad |

### Metadati video nella chiamata introduttiva ad Heartbeat

| Parametro | Valore (esempio)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Metadati standard nella chiamata Avvio annunci Heartbeat

| Parametro | Valore (esempio)  |
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

**Note:**

* Devono essere presenti e contenenti metadati ulteriori variabili di dati di contesto. Consultate i dettagli sui metadati di seguito.
* La lunghezza dell'annuncio può essere impostata su -1 se non è disponibile all'avvio.

### Chiamata completa ad Heartbeat

| Parametro | Valore (esempio)  |
|---|---|
| `s:event:type` | completato |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `l:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `l:stream:type` | vod |
| `s:asset:type` | ad |

### Chiamata di riproduzione heartbeat

| Parametro | Valore (esempio)  |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `l:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `l:stream:type` | vod |
| `s:asset:type` | ad |

## Play main content {#section_u1l_1gf_f2b}

### Chiamata di riproduzione Heartbeat

| Parametro | Valore (esempio)  |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 29 |
| `l:event:duration` | 10189 |
| `l:asset:name` | Titolo episodio |
| `l:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `l:stream:type` | vod |
| `s:asset:type` | main |

**Note:**

* La posizione dell'indicatore di riproduzione deve essere incrementata di 10 con ogni chiamata di riproduzione.
* The `l:event:duration` value represents the number of milliseconds since the last tracking call and should be roughly the same value on each 10 second call.

