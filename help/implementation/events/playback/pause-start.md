---
title: Inizio pausa
description: Segnala che l’utente ha messo in pausa la riproduzione multimediale.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 2%

---


# Inizio pausa

L’evento di avvio della pausa segnala che l’utente ha messo in pausa la riproduzione. Non esiste un evento di ripresa separato; invia un evento [Play](play.md) quando la riproduzione riprende.

* **Prerequisiti**: [Inizio sessione](../session/session-start.md)
* **Metrica associata**: [[!UICONTROL Pause events]](/help/reporting/metrics/pause-events.md)

>[!NOTE]
>
>Non esiste un tipo di evento di ripresa. La ripresa viene dedotta quando si invia un evento [`play`](play.md) dopo `pauseStart`.

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

Chiama [`sendEvent`](https://experienceleague.adobe.com/it/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.pauseStart"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.pauseStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 30
    }
  }
});
```

>[!TAB iOS]

Chiamare `trackPause` quando l&#39;utente mette in pausa la riproduzione.

```swift
tracker.trackPause()
```

>[!TAB Android]

Chiamare `trackPause` quando l&#39;utente mette in pausa la riproduzione.

```kotlin
tracker.trackPause()
```

>[!TAB Roku]

Chiama `sendMediaEvent` con `eventType: "media.pauseStart"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.pauseStart",
        "mediaCollection": {
            "playhead": 30
        }
    }
})
```

>[!TAB API Media Edge]

Chiama l&#39;endpoint [pauseStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/pausestart/):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/pauseStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.pauseStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 30
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

Chiamare `trackPause` quando l&#39;utente mette in pausa la riproduzione:

```javascript
tracker.trackPause();
```

>[!TAB Chromecast]

Chiamare `trackPause` quando l&#39;utente mette in pausa la riproduzione:

```javascript
ADBMobile.media.trackPause();
```

>[!TAB API Media Collection]

Invia un POST `pauseStart` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 30, "ts": 1699523820000 },
  "eventType": "pauseStart"
}
```

>[!ENDTABS]
