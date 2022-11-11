---
title: Dettagli della chiamata di prova
description: Esplora le chiamate da effettuare per convalidare l’implementazione.
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 100%

---

# Dettagli della chiamata di prova {#test-call-details}

## Avvia il lettore multimediale {#start-the-media-player}

### Avvio della chiamata di Adobe Analytics (AppMeasurement) {#aa-start-call}

| Parametro |  Valore (campione)  |
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

* Eventuali variabili di dati di contesto aggiuntive devono essere presenti e contenere metadati. Vedi i dettagli dei metadati qui sotto.
* La lunghezza dei flussi lineari deve essere impostata sulla stima migliore per la visualizzazione corrente.

### Metadati standard nella chiamata iniziale di Adobe Analytics (AppMeasurement) {#std-metadata-aa}

| Parametro |  Valore (campione)  |
|---|---|
| `a.media.show` | Titolo spettacolo |
| `a.media.season` | 6 |
| `a.media.episode` | Titolo episodio |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | commedia |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | casa di produzione |
| `a.media.network` | rete |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | sbloccato |
| `a.media.feed` | nessun feed |
| `a.media.stream_format` | 0 |

### Metadati personalizzati nella chiamata iniziale di Adobe Analytics (AppMeasurement) {#custom-metadata-aa}

| Parametro |  Valore (campione)  |
|---|---|
| `custom.metadataA` | valore |
| `custom.metadataB` | valore |

### Media Analytics (heartbeat): avvio della chiamata {#ma-start-call}

| Parametro |  Valore (campione)  |
|---|---|
| `s:event:type` | inizio |
| _**`l:event:playhead`**_ | _**0**_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Titolo episodio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vago |
| `s:asset:type` | principale |
| _**`s:meta:custom.[value]`**_ | _**Campi di metadati personalizzati**_ |
| _**`s:meta:a.media.[value]`**_ | _**Campi metadati standard**_ |

**Note:**

* Eventuali variabili di dati di contesto aggiuntive devono essere presenti e contenere metadati. Vedi i dettagli dei metadati qui sotto.
* La posizione della testina di riproduzione per i flussi lineari all’avvio del video deve essere impostata sui secondi trascorsi dall’inizio della presentazione corrente, non su 0.

### Metadati standard nella chiamata iniziale di Media Analytics (heartbeat) {#std-metadata-ma}

| Parametro |  Valore (campione)  |
|---|---|
| `s:meta:a.media.show` | Spettacolo |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Titolo episodio |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | commedia |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | casa di produzione |
| `s:meta:a.media.network` | rete |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | sbloccato |
| `s:meta:a.media.feed` | nessun feed |
| `s:meta:a.media.stream_format` | 0 |

### Metadati personalizzati nella chiamata iniziale di Media Analytics (heartbeat) {#custom-metadata-ma}

| Parametro |  Valore (campione)  |
|---|---|
| `s:meta:custom.metadata` | valore |
| `s:meta:custom.metadata` | valore |

### Media Analytics (heartbeat): chiamata iniziale di Adobe Analytics {#ma-aa-start}

| Parametro |  Valore (campione)  |
|---|---|
| _**`s:event:type`**_ | _**aa_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Titolo episodio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vago |
| `s:asset:type` | principale |

**Note:**

* Questa chiamata indica che SDK per contenuti multimediali ha richiesto che una chiamata `pev2=ms_s` sia inviata al server Adobe Analytics (AppMeasurement).
* Questa chiamata non contiene metadati personalizzati.

## Visualizzazione riproduzione annuncio {#view-ad-playback}

### Chiamata inizio annuncio di Adobe Analytics (AppMeasurement) {#aa-ad-start-call}

| Parametro |  Valore (campione)  |
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

* Eventuali variabili di dati di contesto aggiuntive devono essere presenti e contenere metadati. Vedi i dettagli dei metadati qui sotto.
* La lunghezza dell’annuncio può essere impostata su -1 se non è disponibile all’inizio dell’annuncio.

### Metadati standard nella chiamata di inizio annuncio di Adobe Analytics (AppMeasurement) {#std-metadata-aa-ad-start}

| Parametro |  Valore (campione)  |
|---|---|
| `a.media.show` | Titolo spettacolo |
| `a.media.season` | 6 |
| `a.media.episode` | Titolo episodio |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | commedia |
| `a.media.first_air_date` | 04/07/2016 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | casa di produzione |
| `a.media.network` | rete |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | sbloccato |
| `a.media.feed` | nessun feed |
| `a.media.stream_format` | 0 |

### Metadati personalizzati nella chiamata di inizio annuncio di Adobe Analytics (AppMeasurement) {#custom-metadata-aa-ad-start}

| Parametro |  Valore (campione)  |
|---|---|
| `custom.metadata` | valore |
| `custom.metadata` | valore |

### Media Analytics (heartbeat): chiamata inizio annuncio {#ma-ad-start-call}

| Parametro |  Valore (campione)  |
|---|---|
| _**`s:event:type`**_ | _**Inizio**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _**`l:asset:length`**_ | _**120**_ |
| `s:stream:type` | vago |
| _**`s:asset:type`**_ | _**annuncio**_ |
| _**`s:meta:custom.[value]`**_ | _**Campi di metadati personalizzati**_ |
| _**`s:meta:a.media.[value]`**_ | _**Campi metadati standard**_ |

**Note:**

* Eventuali variabili di dati di contesto aggiuntive devono essere presenti e contenere metadati. Vedi i dettagli dei metadati qui sotto.
* La lunghezza dell’annuncio può essere impostata su -1 se non è disponibile all’inizio dell’annuncio.

### Metadati standard nella chiamata di inzio annuncio Media Analytics (heartbeat) {#std-metadata-ma-ad-start}

| Parametro |  Valore (campione)  |
|---|---|
| `s:meta:a.media.show` | Spettacolo |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Titolo episodio |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | commedia |
| `s:meta:a.media.first_air_date` | 04/07/2018 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | casa di produzione |
| `s:meta:a.media.network` | rete |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | sbloccato |
| `s:meta:a.media.feed` | nessun feed |
| `s:meta:a.media.stream_format` | 0 |

### Metadati personalizzati nella chiamata di inzio annuncio Media Analytics (heartbeat) {#custom-metadata-ma-ad-start}

| Parametro |  Valore (campione)  |
|---|---|
| `s:meta:custom.metadata` | valore |
| `s:meta:custom.metadata` | valore |

### Media Analytics (heartbeat): chiamata inizio annuncio di Adobe Analytics {#ma-aa-ad-start-call}

| Parametro |  Valore (campione)  |
|---|---|
| _**`s:event:type`**_ | _**aa_ad_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vago |
| `s:asset:type` | annuncio |

### Chiamata riproduzione annuncio di Media Analytics (heartbeat) {#ma-ad-play-call}

| Parametro |  Valore (campione)  |
|---|---|
| _**`s:event:type`**_ | _**play**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vago |
| _**`s:asset:type`**_ | _**annuncio**_ |

### Media Analytics (heartbeat): chiamata pausa annuncio {#ma-ad-pause-call}

| Parametro |  Valore (campione)  |
|---|---|
| _**`s:event:type`**_ | _**pausa**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vago |
| _**`s:asset:type`**_ | _**annuncio**_ |

### Media Analytics (heartbeat) Chiamata annuncio completo di Adobe Analytics {#ma-aa-ad-complete-call}

| Parametro |  Valore (campione)  |
|---|---|
| _**`s:event:type`**_ | _**completato**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vago |
| _**`s:asset:type`**_ | _**annuncio**_ |

## Riproduci contenuto principale {#play-main-content}

### Media Analytics (heartbeat) Riproduci una chiamata {#ma-play-call}

| Parametro |  Valore (campione)  |
|---|---|
| `s:event:type` | play |
| _**`l:event:playhead`**_ | _**29**_ |
| _**`l:event:duration`**_ | _**10189**_ |
| `s:asset:name` | Titolo episodio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vago |
| `s:asset:type` | principale |

**Note:**

* La posizione della testina di riproduzione dovrebbe aumentare di 10 secondi con ogni chiamata di riproduzione.
* Il valore `l:event:duration` rappresenta il numero di millisecondi trascorsi dall’ultima chiamata di tracciamento e deve corrispondere approssimativamente allo stesso valore per ogni chiamata di 10 secondi.

## Sospendere il contenuto principale {#pause-main-content}

### Media Analytics (heartbeat): chiamata in pausa {#ma-pause-call}

| Parametro |  Valore (campione)  |
|---|---|
| _**`s:event:type`**_ | _**pausa**_ |
| _**`l:event:playhead`**_ | _**29**_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Titolo episodio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vago |
| `s:asset:type` | principale |
