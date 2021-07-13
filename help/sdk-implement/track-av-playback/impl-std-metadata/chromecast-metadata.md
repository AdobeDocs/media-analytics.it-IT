---
title: Spiegazione delle chiavi dei metadati Chromecast
description: Scopri come impostare i video standard e i metadati degli annunci da inviare con le chiamate di tracciamento su Chromecast.
uuid: c446ad41-51b8-46d6-9bc1-abfae866023f
exl-id: ccc717ae-d846-4349-8282-5e3511ddeb9b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 6%

---

# Chiavi dei metadati Chromecast{#chromecast-metadata-keys}

I metadati standard di video e annunci possono essere impostati rispettivamente su oggetti multimediali e informazioni annunci. Utilizzando le chiavi costanti per i metadati video/ad, imposta il dizionario contenente i metadati standard sull&#39;oggetto info prima di richiamare le API di tracciamento. Fai riferimento alle tabelle seguenti per l’intero elenco delle costanti di metadati standard, seguite da un esempio.

## Costanti metadati {#video-metadata-constants}

| Nome metadati | Dati contestuali | Nome costante |
| --- | --- | --- |
| Mostra le informazioni | `a.media.show` | `ADBMobile.media.VideoMetadataKeys.SHOW` |
| Stagione | `a.media.season` | `ADBMobile.media.VideoMetadataKeys.SEASON` |
| Episodio | `a.media.episode` | `ADBMobile.media.VideoMetadataKeys.EPISODE` |
| Risorsa | `a.media.asset` | `ADBMobile.media.VideoMetadataKeys.TMS_ID` |
| Genere | `a.media.genre` | `ADBMobile.media.VideoMetadataKeys.GENRE` |
| Data del primo volo | `a.media.airDate` | `ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE` |
| Prima data dell&#39;aria digitale | `a.media.digitalDate` | `ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE` |
| Valutazione | `a.media.rating` | `ADBMobile.media.VideoMetadataKeys.RATING` |
| Originatore | `a.media.originator` | `ADBMobile.media.VideoMetadataKeys.ORIGINATOR` |
| Rete  | `a.media.network` | `ADBMobile.media.VideoMetadataKeys.NETWORK` |
| Mostra tipo | `a.media.type` | `ADBMobile.media.VideoMetadataKeys.SHOW_TYPE` |
| Caricamento annuncio | `a.media.adLoad` | `ADBMobile.media.VideoMetadataKeys.AD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `ADBMobile.media.VideoMetadataKeys.MVPD` |
| Autorizzato | `a.media.pass.auth` | `ADBMobile.media.VideoMetadataKeys.AUTHORIZED` |
| Parte giorno | `a.media.dayPart` | `ADBMobile.media.VideoMetadataKeys.DAY_PART` |
| Feed | `a.media.feed` | `ADBMobile.media.VideoMetadataKeys.FEED` |
| Formato flusso | `a.media.format` | `ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT` |

## Costanti di metadati degli annunci {#ad-metadata-constants}

| Nome metadati | Dati contestuali | Nome costante |
| --- | --- | --- |
| Inserzionista | `a.media.ad.advertiser` | `ADBMobile.media.AdMetadataKeys.ADVERTISER` |
| ID campagna | `a.media.ad.campaign` | `ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID` |
| ID creativo | `a.media.ad.creative` | `ADBMobile.media.AdMetadataKeys.CREATIVE_ID` |
| ID posizionamento | `a.media.ad.placement` | `ADBMobile.media.AdMetadataKeys.PLACEMENT_ID` |
| ID sito | `a.media.ad.site` | `ADBMobile.media.AdMetadataKeys.SITE_ID` |
| URL creativo | `a.media.ad.creativeURL` | `ADBMobile.media.AdMetadataKeys.CREATIVE_URL` |

## Implementazioni di esempio per Chromecast {#sample-implementations-for-chromecast}

### Video

```js
// setting Standard Video Metadata as context data on trackLoad API mediaContextData = { } 
mediaMetadata["videotype"] = "episode"; 
 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SHOW] = "sample show"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SEASON] = "sample season"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.EPISODE] = "sample episode"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.TMS_ID] = "sample tms_id"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.GENRE] = "sample genre"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE] = "sample first_air_date"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "sample first_digital_date"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.RATING] = "sample rating"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.ORIGINATOR] = "sample originator"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.NETWORK] = "sample network"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SHOW_TYPE] = "sample show type"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.AD_LOAD] = "sample ad load"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.MVPD] = "sample mvpd"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.AUTHORIZED] = "sample authorized"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.DAY_PART] = "sample day_part"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FEED] = "sample feed"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT] = "sample format"; 
 
var mediaObject = ADBMobile.media.createMediaObject(content.name, content.id, content.length, content.streamType); 
mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata; 
ADBMobile.media.trackSessionStart(mediaObject, mediaMetadata); 
```

### Audio

```js
// setting Standard Audio Metadata as context data on trackLoad API mediaContextData = { } 
mediaMetadata["audiotype"] = "podcast"; 
var standardAudioMetadata = {}; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.ARTIST] = “sample artist”; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.ALBUM] = "sample album" ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.LABEL] = "sample label"; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.AUTHOR] = "sample author" ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.STATION] = "sample station " ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.PUBLISHER] = "sample publisher"; 
 
var mediaObject = ADBMobile.media.createMediaObject(content.name, content.id, content.length, content.streamType, content.mediaType); 
mediaObject[ADBMobile.media.MediaObjectKey.StandardAudiooMetadata] = standardAudiooMetadata; 
ADBMobile.media.trackSessionStart(mediaObject, mediaMetadata); 
```

### Annunci

```js
// setting Standard Ad Metadata as context data on ad start event 
var standardAdMetadata = {}; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID] = “sample campaign”; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.ADVERTISER] = "sample advertiser" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_ID] = "sample creativeid"; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.PLACEMENT_ID] = "sample placement id" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.SITE_ID] = "sample site id" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_URL] = "sample creative url"; 
 
var adObject = ADBMobile.media.createAdObject(ad.name, ad.id, ad.position, ad.length); 
adObject[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardVideoMetadata; 
 
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, this._player.getAdInfo(), adContextData);
```
