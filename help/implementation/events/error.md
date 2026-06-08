---
title: Errore
description: Segnala che il lettore multimediale ha riscontrato un errore.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 3%

---


# Errore

L’evento di errore segnala che il lettore multimediale ha riscontrato un errore. Il tracciamento di un errore non chiude la sessione. Se l&#39;errore impedisce il proseguimento della riproduzione, chiamare [Session end](session/session-end.md) dopo l&#39;evento di errore.

* **Prerequisiti**: [Inizio sessione](session/session-start.md)
* **Metrica associata**: [[!UICONTROL Error impacted streams]](/help/reporting/metrics/error-impacted-streams.md)

La proprietà `errorDetails.source` accetta solo due valori: `player` (errori originati nel lettore multimediale) e `external` (errori provenienti da un&#39;origine esterna, ad esempio una rete o una rete CDN).

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.error"` e il `errorDetails` richiesto:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.error",
    mediaCollection: {
      errorDetails: {
        name: "media-error-001",
        source: "player"
      },
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

>[!TAB iOS]

Chiamare `trackError` con una stringa ID errore.

```swift
tracker.trackError(errorId: "media-error-001")
```

>[!TAB Android]

Chiamare `trackError` con una stringa ID errore.

```kotlin
tracker.trackError("media-error-001")
```

>[!TAB Edge Roku]

Chiama `sendMediaEvent` con `eventType: "media.error"` e il `errorDetails` richiesto:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.error",
        "mediaCollection": {
            "errorDetails": {
                "name": "media-error-001",
                "source": "player"
            },
            "playhead": 45
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [error](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/error/) con `errorDetails` richiesto:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/error?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.error",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45,
        "errorDetails": {
          "name": "media-error-001",
          "source": "player"
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Chiamare `trackError` con una stringa ID errore:

```javascript
tracker.trackError("media-error-001");
```

>[!TAB Chromecast]

Chiamare `trackError` con una stringa ID errore:

```javascript
ADBMobile.media.trackError("media-error-001");
```

>[!TAB Roku 2.x]

Chiamare `mediaTrackError` con un ID di errore e l&#39;origine dell&#39;errore. Usa la costante `ERROR_SOURCE_PLAYER` per gli errori del lettore:

```brightscript
adb = ADBMobile()
adb.mediaTrackError("media-error-001", adb.ERROR_SOURCE_PLAYER)
```

>[!TAB API Media Collection]

Invia un POST `error` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "error",
  "params": {
    "media.errorId": "media-error-001",
    "media.errorSource": "player"
  }
}
```

>[!ENDTABS]
