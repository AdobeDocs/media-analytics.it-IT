---
title: Stagione
description: Imposta il numero di stagione per i contenuti episodici in modo che il coinvolgimento possa essere suddiviso per stagione.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 3%

---


# Stagione

>[!BEGINSHADEBOX]

*Questa pagina riguarda la raccolta dati per la variabile **Season**. Vedi [Stagione](/help/reporting/dimensions/season.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile della stagione è il numero della stagione per lo spettacolo (in genere un numero intero di stringa come `"2"`). Impostalo per i contenuti che fanno parte di una serie in modo che il coinvolgimento possa essere suddiviso per stagione. Accoppia con [Show](/help/implementation/variables/standard-metadata/show.md) e [Episode](/help/implementation/variables/standard-metadata/episode.md) per il contesto episodico completo.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.season` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.sessionDetails.season`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.season` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md), chiusura sessione |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `season` all&#39;interno di `xdm.mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        season: "2"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passa la stagione come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.SEASON`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.SEASON] = "2"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Passa la stagione come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.SEASON`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.SEASON] = "2"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

Utilizza `createMediaSession` per impostare `season` in `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "season": "2"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `season` in `xdm.mediaCollection.sessionDetails`:

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
          "season": "2"
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

Passa la stagione nell&#39;oggetto `contextData` utilizzando `ADB.Media.VideoMetadataKeys.Season`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Season] = "2";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Utilizzare `ADBMobile.media.VideoMetadataKeys.SEASON` per impostare il numero di stagione nella proprietà `StandardMediaMetadata` dell&#39;oggetto multimediale prima di chiamare `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.SEASON] = "2";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB API Media Collection]

Includi `media.season` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.season": "2"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).

>[!ENDTABS]
