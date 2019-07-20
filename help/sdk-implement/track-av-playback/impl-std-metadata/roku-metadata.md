---
seo-title: Tasti di metadati Roku
title: Tasti di metadati Roku
uuid: 2 ca 6 bb 1 d-c 545-43 d 3-9 c 3 e -63 b 890 aa 268 d
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Roku metadata keys{#roku-metadata-keys}

I metadati video, audio e degli annunci standard possono essere impostati rispettivamente su supporti e oggetti ad info. Utilizzando le chiavi costanti per i metadati video/annuncio, il dizionario contiene i metadati standard sull'oggetto info prima di richiamare le API di tracciamento. Fate riferimento alle tabelle riportate di seguito per l'elenco completo delle costanti di metadati standard, seguita da un esempio.

## Video metadata constants {#section_D26B0478688D4DC5AEFD82E9AC0F0C0D}

| Nome metadati | Chiave dati contestuali | Nome costante |
| --- | --- | --- |
| Mostra le informazioni | `a.media.show` | `MEDIA_VideoMetadataKeySHOW` |
| Stagione | `a.media.season` | `MEDIA_VideoMetadataKeySEASON` |
| Episodio | `a.media.episode` | `MEDIA_VideoMetadataKeyEPISODE` |
| Risorsa | `a.media.asset` | `MEDIA_VideoMetadataKeyASSET_ID` |
| Genere | `a.media.genre` | `MEDIA_VideoMetadataKeyGENRE` |
| Data prima AIR | `a.media.airDate` | `MEDIA_VideoMetadataKeyFIRST_AIR_DATE` |
| Data prima Digital Air | `a.media.digitalDate` | `MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE` |
| Valutazione | `a.media.rating` | `MEDIA_VideoMetadataKeyRATING` |
| Originator | `a.media.originator` | `MEDIA_VideoMetadataKeyORIGINATOR` |
| Rete | `a.media.network` | `MEDIA_VideoMetadataKeyNETWORK` |
| Mostra tipo | `a.media.type` | `MEDIA_VideoMetadataKeySHOW_TYPE` |
| Caricamento annunci | `a.media.adLoad` | `MEDIA_VideoMetadataKeyAD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `MEDIA_VideoMetadataKeyMVPD` |
| Autorizzato | `a.media.pass.auth` | `MEDIA_VideoMetadataKeyAUTHORIZED` |
| Part Part | `a.media.dayPart` | `MEDIA_VideoMetadataKeyDAY_PART` |
| Feed | `a.media.feed` | `MEDIA_VideoMetadataKeyFEED` |
| Formato flusso | `a.media.format` | `MEDIA_VideoMetadataKeySTREAM_FORMAT` |

## Audio metadata constants {#audio-metadata-constants}

| Nome metadati | Chiave dati contestuali | Nome costante |
| --- | --- | --- |
| Artista | `a.media.artist` | `MEDIA_AudioMetadataKeyARTIST` |
| Album | `a.media.album` | `MEDIA_AudioMetadataKeyALBUM` |
| Etichetta | `a.media.label` | `MEDIA_AudioMetadataKeyLABEL` |
| Autore | `a.media.author` | `MEDIA_AudioMetadataKeyAUTHOR` |
| Stazione | `a.media.station` | `MEDIA_AudioMetadataKeySTATION` |
| Editore | `a.media.publisher` | `MEDIA_AudioMetadataKeyPUBLISHER` |

## Ad metadata constants {#section_5290E1BA54A24D30875F4F55C6CF9458}

| Nome metadati | Chiave dati contestuali | Nome costante |
| --- | --- | --- |
| Inserzionista | `a.media.ad.advertiser` | `MEDIA_AdMetadataKeyADVERTISER` |
| ID campagna | `a.media.ad.campaign` | `MEDIA_AdMetadataKeyCAMPAIGN_ID` |
| ID creativo | `a.media.ad.creative` | `MEDIA_AdMetadataKeyCREATIVE_ID` |
| ID posizionamento | `a.media.ad.placement` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| ID sito | `a.media.ad.site` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| URL creativo | `a.media.ad.creativeURL` | `MEDIA_AdMetadataKeyCREATIVE_URL` |

## Costanti {#section_F55145DBE77F45B988849C42C044C7DA}

Per tenere traccia degli eventi multimediali potete utilizzare le seguenti costanti:

### Altre costanti

| Costante | Descrizione   |
|---|---|
| `ERROR_SOURCE_PLAYER` | Costante per l'origine errore come lettore |

### Costanti mediaobjectkey (utilizzate come chiavi nelle istanze mediaobject)

| Costante | Descrizione   |
| --- | --- |
| `MEDIA_STANDARD_MEDIA_METADATA` | Constant to set metadata on the `MediaInfo` `trackLoad` |
| `MEDIA_STANDARD_AD_METADATA` | Constant to set the ad metadata on the `EventData` `trackEvent` |
| `MEDIA_RESUMED` | Costante per l'invio di un heartbeat ripreso dal video. To resume video tracking of previously stopped content, you need to set the `MEDIA_RESUMED` property on the `mediaInfo` object when you call `mediaTrackLoad`. (`MEDIA_RESUMED` is not an event that you can track using the `mediaTrackEvent` API.) `MEDIA_RESUMED` devono essere impostate su true quando un'applicazione desidera continuare a tracciare il contenuto che un utente ha interrotto guardando ma ora intende riprendere la visualizzazione. <br/><br/>Ad esempio, supponiamo che un utente visualizzi il 30% dei contenuti e quindi la chiuda. Questo porterà la sessione alla fine. Later, if the same user returns to the same content, and the application allows that user to resume from the same point where they left off, then the application should set `MEDIA_RESUMED` to "true" while calling the `mediaTrackLoad` API. Il risultato è che queste due sessioni multimediali diverse per lo stesso contenuto video possono essere collegate insieme. Following is the implementation example: <br/><br/> `mediaInfo =` <br/>   `adb_media_init_mediainfo(` <br/>     `"test_media_name",` <br/>     `"test_media_id",`<br/>      `10,` <br/>     `"vod"` <br/> `)` <br/> `mediaInfo[ADBMobile().MEDIA_RESUMED] = true` <br/> `mediaContextData = {}` <br/>  `ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)`<br/><br/>In tal modo viene creata una nuova sessione per il video, ma anche l'SDK invia una richiesta heartbeat con il tipo di evento "resume", che può essere utilizzato nei report per collegare insieme due diverse sessioni multimediali. |

### Costanti di tipo contenuto

| Costante | Descrizione   |
|---|---|
| `MEDIA_STREAM_TYPE_LIVE` | Costante per tipo di flusso LIVE |
| `MEDIA_STREAM_TYPE_VOD` | Costante per tipo di flusso VOD |

### Costanti di tipo evento (utilizzate per la chiamata trackevent)

| Costante | Descrizione   |
|---|---|
| `MEDIA_BUFFER_START` | Tipo di evento per Inizio buffer |
| `MEDIA_BUFFER_COMPLETE` | Tipo evento completato per il buffer |
| `MEDIA_SEEK_START` | Tipo di evento per Seek Start |
| `MEDIA_SEEK_COMPLETE` | Tipo evento per Ricerca completata |
| `MEDIA_BITRATE_CHANGE` | Tipo di evento per modifica bitrate |
| `MEDIA_CHAPTER_START` | Tipo di evento per Inizio capitolo |
| `MEDIA_CHAPTER_COMPLETE` | Tipo evento per completamento capitolo |
| `MEDIA_CHAPTER_SKIP` | Tipo di evento per Avvio ad |
| `MEDIA_AD_BREAK_START` | Tipo di evento per Avvio ad |
| `MEDIA_AD_BREAK_COMPLETE` | Tipo evento per adbreak Complete |
| `MEDIA_AD_BREAK_SKIP` | Tipo evento per adbreak Skip(Ignora) |
| `MEDIA_AD_START` | Tipo di evento per Avvio ad |
| `MEDIA_AD_COMPLETE` | Tipo evento per Ad Complete |
| `MEDIA_AD_SKIP` | Tipo evento per Ad Skip |

