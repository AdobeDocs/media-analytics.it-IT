---
seo-title: Roku metadata keys
title: Tasti di metadati Roku
uuid: 2ca6bb1d-c545-43d3-9c3e-63b890aa268d
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Tasti di metadati Roku{#roku-metadata-keys}

I metadati video, audio e degli annunci standard possono essere impostati rispettivamente sugli oggetti multimediali e sulle informazioni degli annunci. Utilizzando le chiavi costanti per i metadati video/ad, impostate il dizionario contenente i metadati standard sull'oggetto info prima di chiamare le API track. Per l’elenco completo delle costanti di metadati standard, consultate le tabelle di seguito, seguite da un esempio.

## Costanti di metadati video {#section_D26B0478688D4DC5AEFD82E9AC0F0C0D}

| Nome metadati | Chiave dati contestuali | Nome costante |
| --- | --- | --- |
| Mostra le informazioni | `a.media.show` | `MEDIA_VideoMetadataKeySHOW` |
| Stagione | `a.media.season` | `MEDIA_VideoMetadataKeySEASON` |
| Episodio | `a.media.episode` | `MEDIA_VideoMetadataKeyEPISODE` |
| Risorsa | `a.media.asset` | `MEDIA_VideoMetadataKeyASSET_ID` |
| Genere | `a.media.genre` | `MEDIA_VideoMetadataKeyGENRE` |
| Data primo Air | `a.media.airDate` | `MEDIA_VideoMetadataKeyFIRST_AIR_DATE` |
| Prima data aria digitale | `a.media.digitalDate` | `MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE` |
| Valutazione | `a.media.rating` | `MEDIA_VideoMetadataKeyRATING` |
| Creatore | `a.media.originator` | `MEDIA_VideoMetadataKeyORIGINATOR` |
| Rete | `a.media.network` | `MEDIA_VideoMetadataKeyNETWORK` |
| Mostra tipo | `a.media.type` | `MEDIA_VideoMetadataKeySHOW_TYPE` |
| Caricamento annuncio | `a.media.adLoad` | `MEDIA_VideoMetadataKeyAD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `MEDIA_VideoMetadataKeyMVPD` |
| Autorizzato | `a.media.pass.auth` | `MEDIA_VideoMetadataKeyAUTHORIZED` |
| Parte giorno | `a.media.dayPart` | `MEDIA_VideoMetadataKeyDAY_PART` |
| Feed | `a.media.feed` | `MEDIA_VideoMetadataKeyFEED` |
| Formato flusso | `a.media.format` | `MEDIA_VideoMetadataKeySTREAM_FORMAT` |

## Costanti di metadati audio {#audio-metadata-constants}

| Nome metadati | Chiave dati contestuali | Nome costante |
| --- | --- | --- |
| Artista | `a.media.artist` | `MEDIA_AudioMetadataKeyARTIST` |
| Album | `a.media.album` | `MEDIA_AudioMetadataKeyALBUM` |
| Etichetta | `a.media.label` | `MEDIA_AudioMetadataKeyLABEL` |
| Autore | `a.media.author` | `MEDIA_AudioMetadataKeyAUTHOR` |
| Stazione | `a.media.station` | `MEDIA_AudioMetadataKeySTATION` |
| Publisher | `a.media.publisher` | `MEDIA_AudioMetadataKeyPUBLISHER` |

## Aggiungi costanti di metadati {#section_5290E1BA54A24D30875F4F55C6CF9458}

| Metadata Name | Chiave dati contestuali | Constant Name |
| --- | --- | --- |
| Inserzionista | `a.media.ad.advertiser` | `MEDIA_AdMetadataKeyADVERTISER` |
| Campaign ID | `a.media.ad.campaign` | `MEDIA_AdMetadataKeyCAMPAIGN_ID` |
| Creative ID | `a.media.ad.creative` | `MEDIA_AdMetadataKeyCREATIVE_ID` |
| Placement ID | `a.media.ad.placement` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| ID sito | `a.media.ad.site` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| URL creativo | `a.media.ad.creativeURL` | `MEDIA_AdMetadataKeyCREATIVE_URL` |

## Costanti {#section_F55145DBE77F45B988849C42C044C7DA}

Per tenere traccia degli eventi multimediali potete usare le seguenti costanti:

### Altre costanti

| Costante | Descrizione   |
|---|---|
| `ERROR_SOURCE_PLAYER` | Costante per il lettore della fonte di errore |

### Costanti MediaObject (utilizzate come chiavi nelle istanze MediaObject)

| Costante | Descrizione   |
| --- | --- |
| `MEDIA_STANDARD_MEDIA_METADATA` | Costante per impostare i metadati sul `MediaInfo``trackLoad` |
| `MEDIA_STANDARD_AD_METADATA` | Costante per impostare i metadati dell'annuncio sul pannello `EventData``trackEvent` |
| `MEDIA_RESUMED` | Costante per l’invio di heartbeat ripreso video. Per riprendere il tracciamento video del contenuto precedentemente interrotto, è necessario impostare la `MEDIA_RESUMED` proprietà sull’ `mediaInfo` oggetto al momento della chiamata `mediaTrackLoad`. (`MEDIA_RESUMED` non è un evento che puoi monitorare utilizzando l' `mediaTrackEvent` API). `MEDIA_RESUMED` deve essere impostato su true quando un'applicazione desidera continuare a monitorare il contenuto che un utente ha interrotto ma che intende riprendere la visualizzazione. <br/><br/>Ad esempio, se un utente guarda il 30% del contenuto, chiude l'app. In questo modo la sessione verrà terminata. In seguito, se lo stesso utente torna allo stesso contenuto e l'applicazione consente all'utente di riprendere dallo stesso punto in cui l'ha interrotto, l'applicazione deve impostare `MEDIA_RESUMED` "true" mentre chiama l' `mediaTrackLoad` API. Il risultato è che queste due diverse sessioni multimediali per lo stesso contenuto video possono essere collegate tra loro. Esempio di implementazione: <br/><br/> `mediaInfo =` <br/>   `adb_media_init_mediainfo(` <br/>     `"test_media_name",` <br/>     `"test_media_id",`<br/>      `10,` <br/>     `"vod"` <br/> `)` <br/> `mediaInfo[ADBMobile().MEDIA_RESUMED] = true` <br/> `mediaContextData = {}` <br/>  `ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)` In <br/><br/>questo modo verrà creata una nuova sessione per il video, ma l’SDK invierà anche una richiesta heartbeat con il tipo di evento "curriculum", che può essere utilizzato nel reporting per collegare insieme due diverse sessioni multimediali. |

### Costanti del tipo di contenuto

| Costante | Descrizione   |
|---|---|
| `MEDIA_STREAM_TYPE_LIVE` | Costante per tipo di flusso LIVE |
| `MEDIA_STREAM_TYPE_VOD` | Costante per il tipo di flusso VOD |

### Costanti del tipo di evento (utilizzate per la chiamata trackEvent)

| Costante | Descrizione   |
|---|---|
| `MEDIA_BUFFER_START` | Tipo evento per avvio buffer |
| `MEDIA_BUFFER_COMPLETE` | Tipo evento per Buffer Complete |
| `MEDIA_SEEK_START` | Tipo di evento per la ricerca |
| `MEDIA_SEEK_COMPLETE` | Tipo evento per ricerca completa |
| `MEDIA_BITRATE_CHANGE` | Tipo evento per modifica bitrate |
| `MEDIA_CHAPTER_START` | Event Type for Chapter Start |
| `MEDIA_CHAPTER_COMPLETE` | Tipo evento per il capitolo completo |
| `MEDIA_CHAPTER_SKIP` | Event Type for Ad Start |
| `MEDIA_AD_BREAK_START` | Tipo evento per Ad Start |
| `MEDIA_AD_BREAK_COMPLETE` | Tipo evento per AdBreak Complete |
| `MEDIA_AD_BREAK_SKIP` | Tipo di evento per AdBreak Skip |
| `MEDIA_AD_START` | Tipo evento per Ad Start |
| `MEDIA_AD_COMPLETE` | Tipo evento per annuncio completo |
| `MEDIA_AD_SKIP` | Tipo evento per Salto annuncio |

