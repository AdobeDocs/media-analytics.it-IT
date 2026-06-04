---
title: Tipo di caricamento dell’annuncio
description: Imposta il tipo di caricamento dell’annuncio per la sessione di streaming.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 2%

---


# Tipo di caricamento dell’annuncio

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Ad Load type**. Vedi [Caricamenti annuncio](/help/reporting/dimensions/ad-load-type.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile del tipo di caricamento dell’annuncio identifica il tipo di annuncio caricato all’inizio della sessione. Questo valore è definito dal sistema interno di consegna degli annunci della tua organizzazione e non è vincolato a un’enumerazione standard. Puoi utilizzare qualsiasi stringa significativa per l&#39;implementazione, ad esempio `"linear"`, `"dynamic"` o `"programmatic"`.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.adLoad` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.sessionDetails.adLoad`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.adLoad` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md), chiusura sessione |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `adLoad` all&#39;interno di `xdm.mediaCollection.sessionDetails` quando chiama [`createMediaSession`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/createmediasession):

```javascript
alloy("createMediaSession", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "My Video",
        length: 300,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        adLoad: "linear"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passa il tipo di caricamento dell&#39;annuncio come chiave dei metadati nell&#39;argomento del dizionario a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.AD_LOAD`.

```swift
var videoMetadata: [String: String] = [:]
videoMetadata[MediaConstants.VideoMetadataKeys.AD_LOAD] = "linear"

tracker.trackSessionStart(info: mediaObject, metadata: videoMetadata)
```

>[!TAB Android]

Passa il tipo di caricamento dell&#39;annuncio come chiave dei metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.AD_LOAD`.

```kotlin
val videoMetadata = HashMap<String, String>()
videoMetadata[MediaConstants.VideoMetadataKeys.AD_LOAD] = "linear"

tracker.trackSessionStart(mediaInfo, videoMetadata)
```

>[!TAB Roku]

Utilizza `createMediaSession` per impostare `adLoad` in `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "adLoad": "linear"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `adLoad` in `xdm.mediaCollection.sessionDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 300,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "adLoad": "linear"
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

Passa il tipo di caricamento dell&#39;annuncio nell&#39;oggetto `contextData` utilizzando `ADB.Media.VideoMetadataKeys.AdLoad`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.AdLoad] = "linear";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Utilizzare `ADBMobile.media.VideoMetadataKeys.AD_LOAD` per impostare il tipo di caricamento dell&#39;annuncio nella proprietà `StandardMediaMetadata` dell&#39;oggetto multimediale prima di chiamare `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 300,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.AD_LOAD] = "linear";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB API Media Collection]

Includi `media.adLoad` nell&#39;oggetto `params` della richiesta POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.adLoad": "linear"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).

>[!ENDTABS]
