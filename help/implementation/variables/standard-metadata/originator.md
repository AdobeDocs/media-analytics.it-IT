---
title: Iniziatore
description: Imposta il creatore o lo studio di produzione del contenuto.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 4%

---


# Iniziatore

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Originator**. Vedi [Iniziatore](/help/reporting/dimensions/originator.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile del creatore è il creatore o lo studio di produzione del contenuto (ad esempio, `"Warner Brothers"`, `"Sony"` o `"Disney"`). Utilizzalo per confrontare il coinvolgimento tra proprietari di contenuti o titolari di diritti.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.originator` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.sessionDetails.originator`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.originator` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md), chiusura sessione |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `originator` all&#39;interno di `xdm.mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        originator: "Warner Brothers"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passa il creatore come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.ORIGINATOR`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.ORIGINATOR] = "Warner Brothers"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Passa il creatore come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.ORIGINATOR`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.ORIGINATOR] = "Warner Brothers"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

Utilizza `createMediaSession` per impostare `originator` in `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "originator": "Warner Brothers"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `originator` in `xdm.mediaCollection.sessionDetails`:

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
          "originator": "Warner Brothers"
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

Passa il mittente nell&#39;oggetto `contextData` utilizzando `ADB.Media.VideoMetadataKeys.Originator`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Originator] = "Warner Brothers";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Utilizzare `ADBMobile.media.VideoMetadataKeys.ORIGINATOR` per impostare l&#39;iniziatore nella proprietà `StandardMediaMetadata` dell&#39;oggetto multimediale prima di chiamare `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.ORIGINATOR] = "Warner Brothers";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB API Media Collection]

Includi `media.originator` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.originator": "Warner Brothers"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).

>[!ENDTABS]
