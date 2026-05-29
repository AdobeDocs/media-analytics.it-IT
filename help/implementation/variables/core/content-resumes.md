---
title: Riprende il contenuto
description: Contrassegna una sessione che riprende una riproduzione precedentemente interrotta in modo che il backend conteggi un evento Riprende contenuto.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 3%

---


# Riprende il contenuto

>[!BEGINSHADEBOX]

*In questa pagina viene illustrata la raccolta dati per la variabile **Content resumes**. Vedere [[!UICONTROL Content resumes]](/help/reporting/metrics/content-resumes.md) per la metrica di reporting corrispondente.*

>[!ENDSHADEBOX]

Il contenuto riprende la variabile contrassegna una sessione che riprende una riproduzione precedentemente interrotta. Impostarlo su `media.sessionStart` in modo che il backend conteggi un evento [[!UICONTROL Content resumes]](/help/reporting/metrics/content-resumes.md) per la sessione e lo escluda dai conteggi dei nuovi flussi. Per le implementazioni API direct API e Edge, il client è responsabile del rilevamento delle sessioni riprese (ad esempio, dopo un buffer, una pausa o un arresto superiore a 30 minuti) e dell’impostazione di questo flag di conseguenza.

| Proprietà | Valore |
| --- | --- |
| **Variabile di dati di contesto** | `a.media.resume` |
| **Campo raccolta XDM** | [`xdm.mediaCollection.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caratteristica Audience Manager** | N/D |
| **Obbligatorio** | No |
| **Inviato con** | [Inizio sessione](/help/implementation/events/session/session-start.md) |

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Imposta `hasResume` su `true` all&#39;interno di `xdm.mediaCollection.sessionDetails` quando chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview) per la sessione ripresa:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video",
        hasResume: true
      },
      playhead: 60
    }
  }
});
```

>[!TAB iOS]

Passa il flag di ripresa come parte del bundle di configurazione opzionale dell&#39;oggetto multimediale su `trackSessionStart`. Utilizza la chiave `MediaConstants.MediaObjectKey.RESUMED`.

```swift
var mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)
mediaObject?[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Passa il flag di ripresa come parte del bundle di configurazione opzionale dell&#39;oggetto multimediale su `trackSessionStart`. Utilizza la chiave `MediaConstants.MediaObjectKey.RESUMED`.

```kotlin
val mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)
mediaInfo[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku]

Imposta `hasResume` su `true` all&#39;interno di `xdm.mediaCollection.sessionDetails` quando chiama `createMediaSession` per la sessione ripresa:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video",
                "hasResume": true
            },
            "playhead": 60
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) con `hasResume` impostato su `true` in `xdm.mediaCollection.sessionDetails`:

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
          "hasResume": true
        },
        "playhead": 60
      }
    }
  }]
}
```

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Impostare la chiave `RESUMED` sull&#39;oggetto informazioni multimediali prima di chiamare `trackSessionStart`:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);
mediaInfo[ADB.Media.MediaObjectKey.Resumed] = true;

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Imposta `MediaResumed` sull&#39;oggetto informazioni multimediali prima di chiamare `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
mediaInfo[ADBMobile.media.MediaObjectKey.MediaResumed] = true;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB API Media Collection]

Includi `media.resume` nell&#39;oggetto `params` della richiesta POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.resume": true
  }
}
```

Per la struttura completa delle richieste, consulta il [Riferimento sessioni API di Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md).

>[!ENDTABS]
