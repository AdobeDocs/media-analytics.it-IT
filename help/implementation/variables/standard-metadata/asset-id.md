---
title: ID risorsa
description: Imposta l’ID della risorsa, un identificatore di settore stabile per la risorsa multimediale come un EIDR o un ID TMS/Gracenote.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 3%

---


# ID risorsa

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **ID risorsa**. Vedi [ID risorsa](/help/reporting/dimensions/asset-id.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile ID risorsa è l’identificatore univoco della risorsa multimediale sottostante (ad esempio, un ID episodio, un ID filmato o un ID evento live). In genere proviene da autorità di metadati come EIDR, TMS/Gracenote o Rovi, ma sono accettati anche ID proprietari o interni. Utilizzalo quando devi confrontare il coinvolgimento tra piattaforme di distribuzione che possono assegnare ID di contenuto diversi alla stessa risorsa sottostante.

>[!NOTE]
>
>Il campo della raccolta XDM utilizza `ID` in maiuscolo: `assetID`.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.asset` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.sessionDetails.assetID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.asset` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md), chiusura sessione |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `assetID` all&#39;interno di `xdm.mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        assetID: "89745363"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passa l&#39;ID risorsa come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.ASSET_ID`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Passa l&#39;ID risorsa come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.ASSET_ID`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Edge Roku]

Utilizza `createMediaSession` per impostare `assetID` in `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "assetID": "89745363"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `assetID` in `xdm.mediaCollection.sessionDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "assetID": "89745363"
        },
        "playhead": 0
      }
    }
  }]
}
```

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Passa l&#39;ID risorsa nell&#39;oggetto `contextData` utilizzando `ADB.Media.VideoMetadataKeys.AssetId`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.AssetId] = "89745363";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Utilizzare `ADBMobile.media.VideoMetadataKeys.ASSET_ID` per impostare l&#39;ID risorsa nella proprietà `StandardMediaMetadata` dell&#39;oggetto multimediale prima di chiamare `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.ASSET_ID] = "89745363";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Utilizzare `MEDIA_VideoMetadataKeyASSET_ID` per impostare l&#39;ID risorsa nei metadati standard dell&#39;oggetto multimediale prima di chiamare `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyASSET_ID] = "89745363"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API Media Collection]

Includi `media.assetId` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.assetId": "89745363"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).

>[!ENDTABS]
