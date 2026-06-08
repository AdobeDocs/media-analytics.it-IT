---
title: Autorizzato
description: Segnala una sessione come autenticata tramite Adobe Pass in modo che venga conteggiata nell’evento Autorizzato.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 3%

---


# Autorizzato

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Authorized**. Vedi [Autorizzato](/help/reporting/metrics/authorized.md) per la metrica di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile authorized contrassegna una sessione il cui utente è stato autorizzato tramite Adobe Pass/TV-Everywhere. Impostarlo su `"TRUE"` quando l&#39;autorizzazione viene confermata; in caso contrario, non impostarlo. Associa [MVPD](/help/implementation/variables/standard-metadata/mvpd.md) per interrompere l&#39;autenticazione per provider.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.pass.auth` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.sessionDetails.authorized`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.pass.auth` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md), chiusura sessione |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `authorized` all&#39;interno di `xdm.mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        authorized: "TRUE"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passa il flag authorized come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.AUTHORIZED`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.AUTHORIZED] = "TRUE"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Passa il flag authorized come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.AUTHORIZED`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.AUTHORIZED] = "TRUE"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Edge Roku]

Utilizza `createMediaSession` per impostare `authorized` in `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "authorized": "TRUE"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `authorized` in `xdm.mediaCollection.sessionDetails`:

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
          "authorized": "TRUE"
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

Passa il contrassegno autorizzato nell&#39;oggetto `contextData` utilizzando `ADB.Media.VideoMetadataKeys.Authorized`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Authorized] = "TRUE";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Utilizzare `ADBMobile.media.VideoMetadataKeys.AUTHORIZED` per impostare il contrassegno autorizzato nella proprietà `StandardMediaMetadata` dell&#39;oggetto multimediale prima di chiamare `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.AUTHORIZED] = "TRUE";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Utilizzare `MEDIA_VideoMetadataKeyAUTHORIZED` per impostare il contrassegno autorizzato nei metadati standard dell&#39;oggetto multimediale prima di chiamare `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyAUTHORIZED] = "TRUE"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API Media Collection]

Includi `media.pass.auth` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.pass.auth": "TRUE"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).

>[!ENDTABS]
