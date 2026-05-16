---
title: MVPD
description: Imposta il distributore di programmazione video multicanale quando l’utente si autentica tramite Adobe Pass.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 7%

---


# MVPD

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **MVPD**. Vedi [MVPD](/help/reporting/dimensions/mvpd.md) per la dimensione di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile MVPD (Multichannel Video Programming Distribor) è il provider via cavo, satellite o MVPD virtuale tramite il quale l&#39;utente ha eseguito l&#39;autenticazione, ad esempio `"Comcast"`, `"DirecTV"` o `"YouTubeTV"`. Impostalo quando il contenuto viene inviato dietro l’autenticazione Adobe Pass o TV-Everywhere. Associa [Authorized](/help/implementation/variables/standard-metadata/authorized.md) per tenere traccia delle sessioni che hanno completato l&#39;autenticazione.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.pass.mvpd` |
| **Campo raccolta XDM** | [`mediaCollection.sessionDetails.mvpd`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caratteristica Audience Manager** | `c_contextdata.a.media.pass.mvpd` |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md), chiusura sessione |

## Web SDK

Imposta `mvpd` all&#39;interno di `mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        mvpd: "Comcast"
      },
      playhead: 0
    }
  }
});
```

## Mobile SDK

Passa il MVPD come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.MVPD`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Cotlino)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilizza `createMediaSession` per impostare `mvpd` in `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "mvpd": "Comcast"
            },
            "playhead": 0
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `mvpd` in `mediaCollection.sessionDetails`:

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
          "mvpd": "Comcast"
        },
        "playhead": 0
      }
    }
  }]
}
```

## Media SDK

Passa il MVPD nell&#39;oggetto `contextData` utilizzando `ADB.Media.VideoMetadataKeys.MVPD`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.MVPD] = "Comcast";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Includi `media.pass.mvpd` nell&#39;oggetto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.pass.mvpd": "Comcast"
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).
