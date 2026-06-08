---
title: Episodio
description: Impostare il numero di episodio per il contenuto episodico in modo che i singoli episodi possano essere riportati separatamente.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 3%

---


# Episodio

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Episodio**. Vedi [Episodio](/help/reporting/dimensions/episode.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile dell&#39;episodio è il numero dell&#39;episodio all&#39;interno della stagione (in genere un numero intero di stringa come `"13"`). Accoppia con [Show](/help/implementation/variables/standard-metadata/show.md) e [Season](/help/implementation/variables/standard-metadata/season.md) in modo che il coinvolgimento possa essere suddiviso per singolo episodio.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.episode` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.sessionDetails.episode`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.episode` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md), chiusura sessione |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `episode` all&#39;interno di `xdm.mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        episode: "13"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passa il numero dell&#39;episodio come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.EPISODE`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.EPISODE] = "13"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Passa il numero dell&#39;episodio come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.EPISODE`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.EPISODE] = "13"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Edge Roku]

Utilizza `createMediaSession` per impostare `episode` in `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "episode": "13"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `episode` in `xdm.mediaCollection.sessionDetails`:

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
          "episode": "13"
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

Passa l&#39;episodio nell&#39;oggetto `contextData` utilizzando `ADB.Media.VideoMetadataKeys.Episode`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Episode] = "13";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Utilizzare `ADBMobile.media.VideoMetadataKeys.EPISODE` per impostare il numero di episodio nella proprietà `StandardMediaMetadata` dell&#39;oggetto multimediale prima di chiamare `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.EPISODE] = "13";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Utilizzare `MEDIA_VideoMetadataKeyEPISODE` per impostare il numero di episodio nei metadati standard dell&#39;oggetto multimediale prima di chiamare `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyEPISODE] = "13"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API Media Collection]

Includi `media.episode` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.episode": "13"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).

>[!ENDTABS]
