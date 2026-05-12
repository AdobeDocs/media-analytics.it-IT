---
title: Autorizzato
description: Segnala una sessione come autenticata tramite Adobe Pass in modo che venga conteggiata nell’evento Autorizzato.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 7%

---


# Autorizzato

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Authorized**. Vedi [Autorizzato](/help/reporting/metrics/authorized.md) per la metrica di reporting corrispondente.*

>[!ENDSHADEBOX]

La variabile authorized contrassegna una sessione il cui utente è stato autorizzato tramite Adobe Pass/TV-Everywhere. Impostarlo su `"TRUE"` quando l&#39;autorizzazione viene confermata; in caso contrario, non impostarlo. Associa [MVPD](/help/implementation/variables/standard-metadata/mvpd.md) per interrompere l&#39;autenticazione per provider.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.pass.auth` |
| **Campo raccolta XDM** | [`mediaCollection.sessionDetails.authorized`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obbligatorio** | No |
| **Inviato con** | Avvio della sessione, chiusura della sessione |

## Web SDK

Imposta `authorized` all&#39;interno di `mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview):

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

## Mobile SDK

Passa il flag authorized come chiave di metadati nell&#39;argomento HashMap a `trackSessionStart`. Usa `MediaConstants.VideoMetadataKeys.AUTHORIZED`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.AUTHORIZED] = "TRUE"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Cotlino)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.AUTHORIZED] = "TRUE"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

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

## API di Media Edge

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `authorized` in `mediaCollection.sessionDetails`:

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

## Media SDK

Passa il contrassegno autorizzato nell&#39;oggetto `contextData` utilizzando `ADB.Media.VideoMetadataKeys.Authorized`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Authorized] = "TRUE";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

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
