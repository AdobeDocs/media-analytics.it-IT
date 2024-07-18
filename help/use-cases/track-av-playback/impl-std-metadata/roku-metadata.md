---
title: Spiegazione delle chiavi metadati Roku
description: Scopri le chiavi metadati Roku disponibili e visualizza l’elenco completo delle costanti di metadati standard.
uuid: 2ca6bb1d-c545-43d3-9c3e-63b890aa268d
exl-id: 687dbaa5-4723-4b3f-ab1e-4d5bf447cddf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 100%

---

# Chiavi metadati Roku{#roku-metadata-keys}

I metadati standard di video, audio e annunci possono essere impostati rispettivamente sugli oggetti informazioni multimediali e annunci. Utilizzando le chiavi costanti per i metadati video/annunci, imposta il dizionario contenente i metadati standard sull’oggetto informazioni prima di richiamare le API di tracciamento. Fai riferimento alle tabelle seguenti per l’elenco completo delle costanti di metadati standard, seguite da un esempio.

## Costanti dei metadati video {#video-metadata-constants}

| Nome dei metadati | Chiave dei dati contestuali | Nome costante |
| --- | --- | --- |
| Spettacolo | `a.media.show` | `MEDIA_VideoMetadataKeySHOW` |
| Stagione | `a.media.season` | `MEDIA_VideoMetadataKeySEASON` |
| Episodio | `a.media.episode` | `MEDIA_VideoMetadataKeyEPISODE` |
| Risorsa | `a.media.asset` | `MEDIA_VideoMetadataKeyASSET_ID` |
| Genere | `a.media.genre` | `MEDIA_VideoMetadataKeyGENRE` |
| Data della prima messa in onda | `a.media.airDate` | `MEDIA_VideoMetadataKeyFIRST_AIR_DATE` |
| Data della prima messa in onda digitale | `a.media.digitalDate` | `MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE` |
| Classificazione | `a.media.rating` | `MEDIA_VideoMetadataKeyRATING` |
| Creatore | `a.media.originator` | `MEDIA_VideoMetadataKeyORIGINATOR` |
| Rete | `a.media.network` | `MEDIA_VideoMetadataKeyNETWORK` |
| Tipo di spettacolo | `a.media.type` | `MEDIA_VideoMetadataKeySHOW_TYPE` |
| Caricamento annuncio | `a.media.adLoad` | `MEDIA_VideoMetadataKeyAD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `MEDIA_VideoMetadataKeyMVPD` |
| Autorizzato | `a.media.pass.auth` | `MEDIA_VideoMetadataKeyAUTHORIZED` |
| Fascia oraria | `a.media.dayPart` | `MEDIA_VideoMetadataKeyDAY_PART` |
| Feed | `a.media.feed` | `MEDIA_VideoMetadataKeyFEED` |
| Formato flusso | `a.media.format` | `MEDIA_VideoMetadataKeySTREAM_FORMAT` |

## Costanti di metadati audio {#audio-metadata-constants}

| Nome dei metadati | Chiave dei dati contestuali | Nome costante |
| --- | --- | --- |
| Artista | `a.media.artist` | `MEDIA_AudioMetadataKeyARTIST` |
| Album | `a.media.album` | `MEDIA_AudioMetadataKeyALBUM` |
| Etichetta | `a.media.label` | `MEDIA_AudioMetadataKeyLABEL` |
| Autore | `a.media.author` | `MEDIA_AudioMetadataKeyAUTHOR` |
| Stazione | `a.media.station` | `MEDIA_AudioMetadataKeySTATION` |
| Editore | `a.media.publisher` | `MEDIA_AudioMetadataKeyPUBLISHER` |

## Costanti di metadati dell’annuncio {#ad-metadata-constants}

| Nome dei metadati | Chiave dei dati contestuali | Nome costante |
| --- | --- | --- |
| Inserzionista | `a.media.ad.advertiser` | `MEDIA_AdMetadataKeyADVERTISER` |
| ID campagna | `a.media.ad.campaign` | `MEDIA_AdMetadataKeyCAMPAIGN_ID` |
| ID creatività | `a.media.ad.creative` | `MEDIA_AdMetadataKeyCREATIVE_ID` |
| ID posizionamento | `a.media.ad.placement` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| ID sito | `a.media.ad.site` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| URL creatività | `a.media.ad.creativeURL` | `MEDIA_AdMetadataKeyCREATIVE_URL` |

## Costanti {#constants}

Per tenere traccia degli eventi multimediali è possibile utilizzare le seguenti costanti:

### Altre costanti

| Costante | Descrizione   |
|---|---|
| `ERROR_SOURCE_PLAYER` | Costante per lettore come origine dell’errore |

### Costanti MediaObjectkey (utilizzate come chiavi all’interno delle istanze MediaObject)

| Costante | Descrizione |
| --- | --- |
| `MEDIA_STANDARD_MEDIA_METADATA` | Costante per impostare i metadati su `MediaInfo` `trackLoad` |
| `MEDIA_STANDARD_AD_METADATA` | Costante per impostare i metadati dell’annuncio su `EventData` `trackEvent` |
| `MEDIA_RESUMED` | Costante per l’invio di un heartbeat relativo al video ripreso. Per riprendere il tracciamento video del contenuto precedentemente interrotto, è necessario impostare la proprietà `MEDIA_RESUMED` sull’oggetto `mediaInfo` quando effettui una chiamata `mediaTrackLoad`. (`MEDIA_RESUMED` non è un evento che può essere tracciato utilizzando l’API `mediaTrackEvent`.) `MEDIA_RESUMED` deve essere impostato su true quando un’applicazione desidera continuare a tracciare il contenuto che un utente ha smesso di guardare ma di cui ora intende riprendere la visione. <br/><br/>Ad esempio, supponiamo che un utente guardi il 30% del contenuto e poi chiuda l’app. Questo porterà al termine della sessione. Successivamente, se lo stesso utente ritorna allo stesso contenuto e l’applicazione gli consente di riprendere dallo stesso punto in cui aveva interrotto, l’applicazione deve impostare `MEDIA_RESUMED` su “true” effettuando una chiamata all’API `mediaTrackLoad`. Pertanto ne consegue che queste due diverse sessioni multimediali per gli stessi contenuti video possono essere collegate tra loro. Di seguito è riportato un esempio di implementazione: <br/><br/> `mediaInfo =` <br/>   `adb_media_init_mediainfo(` <br/>     `"test_media_name",` <br/>     `"test_media_id",`<br/>      `10,` <br/>     `"vod"` <br/> `)` <br/> `mediaInfo[ADBMobile().MEDIA_RESUMED] = true` <br/> `mediaContextData = {}` <br/>  `ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)` <br/><br/>Questo creerà una nuova sessione per il video, ma farà anche sì che l’SDK invii una richiesta heartbeat con il tipo di evento “riprendi” che può essere utilizzata nella generazione di rapporti per collegare due diverse sessioni multimediali. |

### Costanti del tipo di contenuto

| Costante | Descrizione   |
|---|---|
| `MEDIA_STREAM_TYPE_LIVE` | Costante per tipo di flusso LIVE |
| `MEDIA_STREAM_TYPE_VOD` | Costante per tipo flusso VOD |

### Costanti del tipo di evento (utilizzate per la chiamata trackEvent)

| Costante | Descrizione   |
|---|---|
| `MEDIA_BUFFER_START` | Tipo di evento per avvio del buffer |
| `MEDIA_BUFFER_COMPLETE` | Tipo di evento per il completamento del buffer |
| `MEDIA_SEEK_START` | Tipo di evento per inizio della ricerca |
| `MEDIA_SEEK_COMPLETE` | Tipo di evento per il completamento della ricerca |
| `MEDIA_BITRATE_CHANGE` | Tipo di evento per modifica del bitrate |
| `MEDIA_CHAPTER_START` | Tipo di evento per inizio del capitolo |
| `MEDIA_CHAPTER_COMPLETE` | Tipo di evento per capitolo completato |
| `MEDIA_CHAPTER_SKIP` | Tipo di evento per avvio dell’annuncio |
| `MEDIA_AD_BREAK_START` | Tipo di evento per avvio dell’annuncio |
| `MEDIA_AD_BREAK_COMPLETE` | Tipo di evento per pausa annuncio completata |
| `MEDIA_AD_BREAK_SKIP` | Tipo di evento per salta pausa annuncio |
| `MEDIA_AD_START` | Tipo di evento per avvio dell’annuncio |
| `MEDIA_AD_COMPLETE` | Tipo di evento per annuncio completato |
| `MEDIA_AD_SKIP` | Tipo di evento per salta annuncio |
