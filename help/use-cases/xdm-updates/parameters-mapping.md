---
title: Migrare i tipi di pubblico al nuovo tipo di dati Adobe Analytics for Streaming Media
description: Scopri come migrare i tipi di pubblico al nuovo tipo di dati Adobe Analytics for Streaming Media
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: 79203a2f-8158-44f2-83b2-146179be9180
source-git-commit: 61e5279e6d53b18955424e76d05d440b83dae07e
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 42%

---

# Mappatura dei parametri di Media Analytics per Adobe Experience Platform e Customer Journey Analytics

Questo documento fornisce un elenco completo di tutti i parametri di Media Analytics utilizzati in Adobe Experience Platform e Customer Journey Analytics. Il suo scopo è quello di supportare l&#39;integrazione dei dati importati da Adobe Analytics a Platform tramite il [connettore Source Analytics](https://experienceleague.adobe.com/it/docs/experience-platform/sources/connectors/adobe-applications/analytics) o il [connettore Source Analytics per le classificazioni](https://experienceleague.adobe.com/it/docs/experience-platform/sources/connectors/adobe-applications/classifications), mappando ogni parametro al percorso del campo XDM corrispondente.

## Variabili riservate di Media Analytics

Per tutte le variabili riservate di Media Analytics, i dati acquisiti da Adobe Analytics in AEP fino a maggio 2025 (incluso) possono essere trovati nel &quot;Percorso campo XDM corrente&quot; indicato nelle tabelle seguenti.

Poiché i team di Media Analytics e ADC stanno attualmente lavorando alla migrazione completa al &quot;Percorso campo XDM per reporting&quot;, una volta completata la migrazione sarà condivisa una comunicazione ufficiale e sarà disponibile il &quot;Percorso campo XDM per reporting&quot;.

## Parametri per Streaming Media

| Nome campo: | Percorso campo XDM corrente (obsoleto) | Percorso campo XDM per reporting | Tipo di dati | Campo derivato | Note |
|--------------------|---------------------------------------------------------------------------|---------------------------------------------------|-----------|-------------------|-----------------------------------------------------------------------|
| Tipo di flusso | media.mediaTimed.primaryAssetReference.streamType | mediaReporting.sessionDetails.streamType | Dimensione | Tipo di flusso |                                                                       |
| ID contenuto | media.mediaTimed.primaryAssetReference._id | mediaReporting.sessionDetails.name | Dimensione | ID contenuto |                                                                       |
| Durata del contenuto | media.mediaTimed.primaryAssetReference._xmpDM.duration | mediaReporting.sessionDetails.length | Dimensione | Durata del contenuto |                                                                       |
| Tipo di contenuto | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | mediaReporting.sessionDetails.contentType | Dimensione | Tipo di contenuto |                                                                       |
| ID sessione multimediale | media.mediaTimed.primaryAssetViewDetails._id | mediaReporting.sessionDetails.ID | Dimensione | ID sessione multimediale |                                                                       |
| Nome del lettore di contenuti | media.mediaTimed.primaryAssetViewDetails.playerName | mediaReporting.sessionDetails.playerName | Dimensione | Nome del lettore di contenuti |                                                                       |
| Canale del contenuto | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | mediaReporting.sessionDetails.channel | Dimensione | Canale del contenuto |                                                                       |
| Segmento di contenuto | media.mediaTimed.primaryAssetViewDetails.videoSegment | mediaReporting.sessionDetails.segment | Dimensione | Segmento di contenuto |                                                                       |
| Nome del contenuto | media.mediaTimed.primaryAssetReference._dc.title | mediaReporting.sessionDetails.friendlyName | Dimensione | Nome del contenuto |                                                                       |
| Percorso video | *Non utilizzato in AEP/CJA* |                                                   |           |                   | Proprietà specifica di Adobe Analytics |
| Spettacolo | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | mediaReporting.sessionDetails.show | Dimensione | Spettacolo |                                                                       |
| Stagione | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | mediaReporting.sessionDetails.season | Dimensione | Stagione |                                                                       |
| Episodio | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | mediaReporting.sessionDetails.episode | Dimensione | Episodio |                                                                       |
| Genere | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | mediaReporting.sessionDetails.genreList | Dimensione | non supportato | Usa campo mediaReporting |
| Rete | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | mediaReporting.sessionDetails.network | Dimensione | Rete |                                                                       |
| Tipo di spettacolo | media.mediaTimed.primaryAssetReference.showType | mediaReporting.sessionDetails.showType | Dimensione | Tipo di spettacolo |                                                                       |
| MVPD | media.mediaTimed.idp | mediaReporting.sessionDetails.mvpd | Dimensione | MVPD |                                                                       |
| Autorizzato | Non supportati | mediaReporting.sessionDetails.authorized | Dimensione | Autorizzato |                                                                       |
| Fascia oraria | Non supportati | mediaReporting.sessionDetails.dayPart | Dimensione | Fascia oraria |                                                                       |
| Tipo di feed multimediale | media.mediaTimed.primaryAssetViewDetails.sourceFeed | mediaReporting.sessionDetails.feed | Dimensione | Tipo di feed multimediale |                                                                       |
| Artista | media.mediaTimed.primaryAssetReference._xmpDM.artist | mediaReporting.sessionDetails.artist | Dimensione | Artista |                                                                       |
| Album | media.mediaTimed.primaryAssetReference._xmpDM.album | mediaReporting.sessionDetails.album | Dimensione | Album |                                                                       |
| Etichetta | Non supportati | mediaReporting.sessionDetails.label | Dimensione | Etichetta |                                                                       |
| Autore | Non supportati | mediaReporting.sessionDetails.author | Dimensione | Autore |                                                                       |
| Stazione | media.mediaTimed.primaryAssetReference._id3.Audio._id3.TRSN | mediaReporting.sessionDetails.station | Dimensione | Stazione |                                                                       |
| Editore | media.mediaTimed.primaryAssetReference._id3.Audio._id3.TPUB | mediaReporting.sessionDetails.publisher | Dimensione | Editore |                                                                       |
| Avvio file multimediale | media.mediaTimed.impressions.value | mediaReporting.sessionDetails.isViewed | Metrica | Avvio file multimediale |                                                                       |
| Avvio contenuti | media.mediaTimed.starts.value | mediaReporting.sessionDetails.isPlayed | Metrica | Avvio contenuti |                                                                       |
| Completamento contenuto | media.mediaTimed.completes.value | mediaReporting.sessionDetails.isCompleted | Metrica | Completamento contenuto |                                                                       |
| Tempo trascorso dei contenuti | media.mediaTimed.timePlayed.value | mediaReporting.sessionDetails.timePlayed | Metrica | Tempo trascorso dei contenuti |                                                                       |
| Tempo trascorso dei contenuti multimediali | media.mediaTimed.totalTimePlayed.value | mediaReporting.sessionDetails.totalTimePlayed | Metrica | Tempo trascorso dei contenuti multimediali |                                                                       |
| Tempo specifico riprodotto | Non supportati | mediaReporting.sessionDetails.uniqueTimePlayed | Metrica | Tempo specifico riprodotto |                                                                       |
| Marcatore progresso 10% | media.mediaTimed.progress10.value | mediaReporting.sessionDetails.hasProgress10 | Metrica | Marcatore progresso 10% |                                                                       |
| Marcatore progresso 25% | media.mediaTimed.progress25.value | mediaReporting.sessionDetails.hasProgress25 | Metrica | Marcatore progresso 25% |                                                                       |
| Marcatore progresso 50% | media.mediaTimed.progress50.value | mediaReporting.sessionDetails.hasProgress50 | Metrica | Marcatore progresso 50% |                                                                       |
| Marcatore progresso 75% | media.mediaTimed.progress75.value | mediaReporting.sessionDetails.hasProgress75 | Metrica | Marcatore progresso 75% |                                                                       |
| Marcatore progresso 95% | media.mediaTimed.progress95.value | mediaReporting.sessionDetails.hasProgress95 | Metrica | Marcatore progresso 95% |                                                                       |
| Pubblico medio per minuto | Non supportati | mediaReporting.sessionDetails.averageMinuteAudience | Metrica | Pubblico medio per minuto |                                                                  |
| Secondi trascorsi dall’ultima chiamata | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | mediaReporting.sessionDetails.secondsSinceLastCall | Metrica | Secondi trascorsi dall’ultima chiamata |                                                              |
| Flussi interessati in pausa | Non supportati | mediaReporting.sessionDetails.hasPauseImpactedStreams | Metrica | Flussi interessati in pausa | copriamo mediaTimed calcolando questo valore da altri eventi |
| Eventi di pausa | media.mediaTimed.pauses.value | mediaReporting.sessionDetails.pauseCount | Metrica | Eventi di pausa |                                                                       |
| Durata totale pausa | media.mediaTimed.pauseTime.value | mediaReporting.sessionDetails.pauseTime | Metrica | Durata totale pausa |                                                                       |
| Riprende i contenuti | media.mediaTimed.resumes.value | mediaReporting.sessionDetails.hasResume | Metrica | Riprende i contenuti |                                                                       |
| Visualizzazioni segmento di contenuto | media.mediaTimed.mediaSegmentViews.value | mediaReporting.sessionDetails.hasSegmentView | Metrica | Visualizzazioni segmento di contenuto |                                                                     |

{style="table-layout:auto"}

## Aggiornamento dei parametri dello stato del lettore

| Nome campo: | Percorso campo XDM corrente (obsoleto) | Percorso campo XDM per reporting | Tipo di dati | Campo derivato | Note |
|----------------------------|-------------------------------------|----------------------------------|-----------|----------------|--------------------------------------|
| Flussi interessati dagli stati del lettore | Non supportati | mediaReporting.states.isSet | Metrica | non supportato | usa campo mediaReporting |
| Conteggi degli stati del lettore | Non supportati | mediaReporting.states.count | Metrica | non supportato | usa campo mediaReporting |
| Durata totale stati del lettore | Non supportati | mediaReporting.states.time | Metrica | non supportato | usa campo mediaReporting |
| Nome stato lettore | Non supportati | mediaReporting.states.name | Dimensione | non supportato | usa campo mediaReporting |

{style="table-layout:auto"}

## Parametri per i capitoli 

| Nome campo: | Percorso campo XDM corrente (obsoleto) | Percorso campo XDM per reporting | Tipo di dati | Campo derivato | Note |
|------------------|--------------------------------------------------------------|-------------------------------------------|-----------|----------------|-----------|
| Capitolo | media.mediaTimed.mediaChapter.chapterAssetReference._id | mediaReporting.chapterDetails.ID | Dimensione | Capitolo |           |
| Inizio capitolo | media.mediaTimed.mediaChapter.impressions.value | mediaReporting.chapterDetails.isStarted | Metrica | Inizio capitolo |           |
| Capitolo completato | media.mediaTimed.mediaChapter.completes.value | mediaReporting.chapterDetails.isCompleted | Metrica | Capitolo completato |          |
| Tempo trascorso capitolo | media.mediaTimed.mediaChapter.timePlayed.value | mediaReporting.chapterDetails.timePlayed | Metrica | Tempo trascorso capitolo |        |

{style="table-layout:auto"}

## Parametri per gli annunci 

| Nome campo: | Percorso campo XDM corrente (obsoleto) | Percorso campo XDM per reporting | Tipo di dati | Campo derivato | Note |
|------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| ID annuncio | advertising.adAssetReference._id | mediaReporting.advertisingDetails.name | Dimensione | ID annuncio |           |
| Posizione annuncio in pod | advertising.adAssetViewDetails.index | mediaReporting.advertisingDetails.podPosition | Dimensione | Posizione annuncio in pod |     |
| Lunghezza annuncio | advertising.adAssetReference._xmpDM.duration | mediaReporting.advertisingDetails.length | Metrica | Lunghezza annuncio |           |
| Nome del lettore dell’annuncio | advertising.adAssetViewDetails.playerName | mediaReporting.advertisingDetails.playerName | Dimensione | Nome del lettore dell’annuncio |           |
| ID interruzione annuncio | advertising.adAssetViewDetails.adBreak._id | mediaReporting.advertisingPodDetails.ID | Dimensione | ID interruzione annuncio |           |
| Nome annuncio | advertising.adAssetReference._dc.title | mediaReporting.advertisingDetails.friendlyName | Dimensione | Nome annuncio |           |
| Inserzionista | advertising.adAssetReference.advertiser | mediaReporting.advertisingDetails.advertiser | Dimensione | Inserzionista |           |
| ID campagna | advertising.adAssetReference.campaign | mediaReporting.advertisingDetails.campaignID | Dimensione | ID campagna |           |
| Avvio annuncio | advertising.impressions.value | mediaReporting.advertisingDetails.isStarted | Metrica | Avvio annuncio |           |
| Annuncio completato | advertising.completes.value | mediaReporting.advertisingDetails.isCompleted | Metrica | Annuncio completato |           |
| Tempo trascorso dell’annuncio | advertising.timePlayed.value | mediaReporting.advertisingDetails.timePlayed | Metrica | Tempo trascorso dell’annuncio |           |

{style="table-layout:auto"}

## Parametri per la qualità 

| Nome campo: | Percorso campo XDM corrente (obsoleto) | Percorso campo XDM per reporting | Tipo di dati | Campi derivati | Note |
|------------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| Bitrate medio | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage.value | mediaReporting.qoeDataDetails.bitrateAverage | Entrambi | Bitrate medio |           |
| Ora di inizio | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart.value | mediaReporting.qoeDataDetails.timeToStart | Entrambi | Ora di inizio |           |
| Frame rilasciati | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames.value | mediaReporting.qoeDataDetails.droppedFrames | Entrambi | Frame rilasciati |           |
| Eventi buffer | media.mediaTimed.primaryAssetViewDetails.qoe.buffers.value | mediaReporting.qoeDataDetails.bufferCount | Entrambi | Eventi buffer |           |
| Durata totale buffer | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime.value | mediaReporting.qoeDataDetails.bufferTime | Entrambi | Durata totale buffer |     |
| Modifiche bitrate | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges.value | mediaReporting.qoeDataDetails.bitrateChangeCount | Entrambi | Modifiche bitrate |         |
| Errori / Eventi di errore | media.mediaTimed.primaryAssetViewDetails.qoe.errors.value | mediaReporting.qoeDataDetails.errorCount | Entrambi | Errori / Eventi di errore |  |
| ID errore SDK del lettore | media.mediaTimed.primaryAssetViewDetails.qoe.playerSdkErrors | mediaReporting.qoeDataDetails.playerSdkErrors | Dimensione | non supportato | usa campo mediaReporting |
| ID errore esterni | media.mediaTimed.primaryAssetViewDetails.qoe.externalSdkErrors | mediaReporting.qoeDataDetails.externalErrors | Dimensione | non supportato | usa campo mediaReporting |
| Rilasci prima dell’inizio | media.mediaTimed.dropBeforeStarts.value | mediaReporting.qoeDataDetails.isDroppedBeforeStart | Metrica | Rilasci prima dell’inizio |     |
| Flussi interessati dal buffer | Non supportati | mediaReporting.qoeDataDetails.hasBufferImpactedStreams | Metrica | Flussi interessati dal buffer | calcolato da altri eventi |
| Flussi interessati dalla modifica del bitrate | Non supportati | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams | Metrica | Flussi interessati dalla modifica del bitrate | calcolato da altri eventi |
| Flussi interessati dall’errore | Non supportati | mediaReporting.qoeDataDetails.hasErrorImpactedStreams | Metrica | Flussi interessati dall’errore | calcolato da altri eventi |
| Flussi interessati da fotogrammi saltati | Non supportati | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams | Metrica | Flussi interessati da fotogrammi saltati | calcolato da altri eventi |

{style="table-layout:auto"}

## Classificazioni di Media Analytics

Le classificazioni di Media Analytics vengono acquisite in AEP tramite un flusso separato noto come ACDC. Ogni gruppo di classificazione elencato nella tabella seguente corrisponde a un set di dati univoco all’interno di AEP. In CJA, è necessario stabilire una connessione tra il set di dati dell’evento Media Analytics e ciascuno dei set di dati di classificazione.

### Connessione dei set di dati in Customer Journey Analytics

Per impostare la connessione in Customer Journey Analytics:

- Passare alla scheda **Connessioni** e selezionare **Crea nuova connessione**.
- Nell&#39;interfaccia Connessioni, scegli **Aggiungi set di dati** e individua il set di dati dell&#39;evento Media Analytics (utilizzato per l&#39;importazione di dati multimediali tramite ADC), insieme ai quattro set di dati di classificazione rilevanti.

### Dettagli configurazione

Per ogni set di dati di ricerca (set di dati di classificazione), configura come segue:

- **set di dati video**:
   - Chiave: `_sandbox.key`
   - Chiave corrispondente: `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   - Tipo di origine dati: `Web Data`

- **set di dati videoad**:
   - Chiave: `_sandbox.key`
   - Chiave corrispondente: `Ad ID (advertising.adAssetReference._id)`
   - Tipo di origine dati: `Web Data`

- **set di dati videoadpod**:
   - Chiave: `_sandbox.key`
   - Chiave corrispondente: `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   - Tipo di origine dati: `Web Data`

- **set di dati videochapter**:
   - Chiave: `_sandbox.key`
   - Chiave corrispondente: `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   - Tipo di origine dati: `Web Data`

### Considerazioni sul reporting

Quando lavori con i set di dati di classificazione durante il reporting, accertati di fare riferimento ai percorsi dei campi specifici della classificazione (`ACDC XDM Path`) invece dei campi XDM di Media Analytics standard.

## Tabella classificazioni

| Nome classificazione (gruppo) | Nome campo: | Percorso ACDC XDM |
|------------|----------|-------------|
| video | ID chiave/risorsa | `<_sandbox>.key` |
| video | Lunghezza video | `<_sandbox>.video_length` |
| video | Nome del video | `<_sandbox>.video_name` |
| video | ID risorsa | `<_sandbox>.asset_id` |
| video | Data della prima messa in onda | `<_sandbox>.first_air_date` |
| video | Data prima versione digitale | `<_sandbox>.first_digital_date` |
| video | Valutazione dei contenuti | `<_sandbox>.content_rating` |
| video | Creatore | `<_sandbox>.originator` |
| videoad | ID chiave/annuncio | `<_sandbox>.key` |
| videoad | Lunghezza annuncio | `<_sandbox>.ad_length` |
| videoad | Nome annuncio | `<_sandbox>.ad_name` |
| videoad | ID creatività | `<_sandbox>.creative_id` |
| videoadpod | ID chiave/pod annuncio | `<_sandbox>.key` |
| videoadpod | Posizione pod | `<_sandbox>.pod_position` |
| videoadpod | Nome pod | `<_sandbox>.pod_name` |
| videochapter | Chiave/Capitolo | `<_sandbox>.key` |
| videochapter | Durata capitolo | `<_sandbox>.chapter_length` |
| videochapter | Offset del capitolo | `<_sandbox>.chapter_offset` |
| videochapter | Posizione del capitolo | `<_sandbox>.chapter_position` |
| videochapter | Nome del capitolo | `<_sandbox>.chapter_name` |

{style="table-layout:auto"}

## Variabili personalizzate di Media Analytics

In Adobe Analytics, le variabili personalizzate vengono assegnate a eventi o eVar diversi a seconda delle regole di implementazione definite all’interno di ogni suite di rapporti. Di conseguenza, quando queste variabili personalizzate vengono importate in Adobe Experience Platform (AEP), vengono mappate su percorsi XDM diversi.

- Gli eventi sono memorizzati nel percorso:

  `_experience.analytics.event<x>to<y>.event<number>.value`

- Le eVar sono memorizzate nel percorso:

  `_experience.analytics.customDimensions.eVars.eVar<number>`

In entrambi i casi, `<number>` corrisponde all&#39;evento specifico o al numero di eVar utilizzato nella configurazione originale della suite di rapporti di Adobe Analytics.

### Variabili personalizzate

| Nome campo: | Percorso XDM | Tipo di dati |
|-------------|-------------|-----------|
| Contrassegno di contenuto multimediale scaricato | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrica |
| Versione SDK | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensione |
| Versione VHL | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensione |
| Formato flusso | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensione |
| Data della prima messa in onda | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensione |
| Data prima versione digitale | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensione |
| Dati federati | `_experience.analytics.customDimensions.eVars.eVar<number>` e `_experience.analytics.event<x>to<y>.event<number>.value` | Entrambi |
| Flussi stimati | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrica |
| Conteggio annunci | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrica |
| Conteggio capitoli | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrica |
| ID creatività | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensione |
| ID sito | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensione |
| URL creatività | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensione |
| ID posizionamento | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimensione |
| Frame al secondo | `_experience.analytics.customDimensions.eVars.eVar<number>` e `_experience.analytics.event<x>to<y>.event<number>.value` | Entrambi |
| ID errore SDK per contenuti multimediali | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrica |
| Stallo dei flussi interessati | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrica |
| Stallo degli eventi | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrica |
| Durata totale dello stallo | `_experience.analytics.event<x>to<y>.event<number>.value` | Metrica |

{style="table-layout:auto"}
