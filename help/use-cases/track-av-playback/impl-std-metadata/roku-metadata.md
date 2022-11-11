---
title: Spiegazione delle chiavi dei metadati Roku
description: Scopri le chiavi di metadati Roku disponibili e visualizza l’intero elenco delle costanti di metadati standard.
uuid: 2ca6bb1d-c545-43d3-9c3e-63b890aa268d
exl-id: 687dbaa5-4723-4b3f-ab1e-4d5bf447cddf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 10%

---

# Chiavi metadati Roku{#roku-metadata-keys}

I metadati standard di video, audio e annunci possono essere impostati rispettivamente su oggetti multimediali e informazioni annunci. Utilizzando le chiavi costanti per i metadati video/ad, imposta il dizionario contenente i metadati standard sull&#39;oggetto info prima di richiamare le API di tracciamento. Fai riferimento alle tabelle seguenti per l’intero elenco delle costanti di metadati standard, seguite da un esempio.

## Costanti di metadati video {#video-metadata-constants}

| Nome metadati | Dati contestuali | Nome costante |
| --- | --- | --- |
| Spettacolo | `a.media.show` | `MEDIA_VideoMetadataKeySHOW` |
| Stagione | `a.media.season` | `MEDIA_VideoMetadataKeySEASON` |
| Episodio | `a.media.episode` | `MEDIA_VideoMetadataKeyEPISODE` |
| Risorsa | `a.media.asset` | `MEDIA_VideoMetadataKeyASSET_ID` |
| Genere | `a.media.genre` | `MEDIA_VideoMetadataKeyGENRE` |
| Data della prima messa in onda | `a.media.airDate` | `MEDIA_VideoMetadataKeyFIRST_AIR_DATE` |
| Prima data dell&#39;aria digitale | `a.media.digitalDate` | `MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE` |
| Valutazione | `a.media.rating` | `MEDIA_VideoMetadataKeyRATING` |
| Iniziatore | `a.media.originator` | `MEDIA_VideoMetadataKeyORIGINATOR` |
| Rete | `a.media.network` | `MEDIA_VideoMetadataKeyNETWORK` |
| Tipo di spettacolo | `a.media.type` | `MEDIA_VideoMetadataKeySHOW_TYPE` |
| Caricamento annuncio | `a.media.adLoad` | `MEDIA_VideoMetadataKeyAD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `MEDIA_VideoMetadataKeyMVPD` |
| Autorizzato | `a.media.pass.auth` | `MEDIA_VideoMetadataKeyAUTHORIZED` |
| Fascia oraria | `a.media.dayPart` | `MEDIA_VideoMetadataKeyDAY_PART` |
| Feed | `a.media.feed` | `MEDIA_VideoMetadataKeyFEED` |
| Formato flusso | `a.media.format` | `MEDIA_VideoMetadataKeySTREAM_FORMAT` |

## Costanti di metadati audio {#audio-metadata-constants}

| Nome metadati | Dati contestuali | Nome costante |
| --- | --- | --- |
| Artista | `a.media.artist` | `MEDIA_AudioMetadataKeyARTIST` |
| Album | `a.media.album` | `MEDIA_AudioMetadataKeyALBUM` |
| Etichetta | `a.media.label` | `MEDIA_AudioMetadataKeyLABEL` |
| Autore | `a.media.author` | `MEDIA_AudioMetadataKeyAUTHOR` |
| Stazione | `a.media.station` | `MEDIA_AudioMetadataKeySTATION` |
| Autore | `a.media.publisher` | `MEDIA_AudioMetadataKeyPUBLISHER` |

## Costanti di metadati degli annunci {#ad-metadata-constants}

| Nome metadati | Dati contestuali | Nome costante |
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
| `ERROR_SOURCE_PLAYER` | Costante per il lettore della sorgente di errore |

### Costanti MediaObjectKey (utilizzate come chiavi nelle istanze MediaObject)

| Costante | Descrizione   |
| --- | --- |
| `MEDIA_STANDARD_MEDIA_METADATA` | Costante per impostare i metadati sul `MediaInfo` `trackLoad` |
| `MEDIA_STANDARD_AD_METADATA` | Costante per impostare i metadati dell&#39;annuncio sul `EventData` `trackEvent` |
| `MEDIA_RESUMED` | Costante per l’invio di un heartbeat ripreso in video. Per riprendere il tracciamento video del contenuto precedentemente interrotto, è necessario impostare la `MEDIA_RESUMED` sulla proprietà `mediaInfo` oggetto quando si chiama `mediaTrackLoad`. (`MEDIA_RESUMED` non è un evento che può essere monitorato utilizzando `mediaTrackEvent` API) `MEDIA_RESUMED` deve essere impostato su true quando un&#39;applicazione desidera continuare a monitorare il contenuto che un utente ha interrotto la visualizzazione ma che intende riprendere la visualizzazione. <br/><br/>Ad esempio, supponiamo che un utente guardi il 30% del contenuto e poi chiuda l’app. La sessione verrà quindi terminata. Successivamente, se lo stesso utente ritorna allo stesso contenuto e l&#39;applicazione consente all&#39;utente di riprendere dallo stesso punto in cui l&#39;hanno disattivato, l&#39;applicazione deve essere impostata `MEDIA_RESUMED` a &quot;true&quot; mentre si chiama il `mediaTrackLoad` API. Il risultato è che queste due diverse sessioni multimediali per lo stesso contenuto video possono essere collegate tra loro. Di seguito è riportato un esempio di implementazione: <br/><br/> `mediaInfo =` <br/>   `adb_media_init_mediainfo(` <br/>     `"test_media_name",` <br/>     `"test_media_id",`<br/>      `10,` <br/>     `"vod"` <br/> `)` <br/> `mediaInfo[ADBMobile().MEDIA_RESUMED] = true` <br/> `mediaContextData = {}` <br/>  `ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)` <br/><br/>In questo modo si crea una nuova sessione per il video, ma l’SDK invia anche una richiesta heartbeat con il tipo di evento &quot;curriculum&quot;, che può essere utilizzato nel reporting per collegare due diverse sessioni multimediali. |

### Costanti del tipo di contenuto

| Costante | Descrizione   |
|---|---|
| `MEDIA_STREAM_TYPE_LIVE` | Costante per tipo di flusso LIVE |
| `MEDIA_STREAM_TYPE_VOD` | Costante per VOD di tipo flusso |

### Tipo evento Costanti (utilizzato per la chiamata trackEvent)

| Costante | Descrizione   |
|---|---|
| `MEDIA_BUFFER_START` | Tipo evento per avvio buffer |
| `MEDIA_BUFFER_COMPLETE` | Tipo evento per il completamento del buffer |
| `MEDIA_SEEK_START` | Tipo evento per la ricerca |
| `MEDIA_SEEK_COMPLETE` | Tipo evento per ricerca completa |
| `MEDIA_BITRATE_CHANGE` | Tipo evento per modifica bitrate |
| `MEDIA_CHAPTER_START` | Tipo evento per inizio capitolo |
| `MEDIA_CHAPTER_COMPLETE` | Tipo evento per il capitolo completo |
| `MEDIA_CHAPTER_SKIP` | Tipo di evento per Ad Start |
| `MEDIA_AD_BREAK_START` | Tipo di evento per Ad Start |
| `MEDIA_AD_BREAK_COMPLETE` | Tipo evento per AdBreak Complete |
| `MEDIA_AD_BREAK_SKIP` | Tipo di evento per Salto AdBreak |
| `MEDIA_AD_START` | Tipo di evento per Ad Start |
| `MEDIA_AD_COMPLETE` | Tipo evento per completamento annuncio |
| `MEDIA_AD_SKIP` | Tipo evento per Salto annuncio |
