---
title: Fine sessione
description: Chiudi immediatamente una sessione multimediale quando il visualizzatore abbandona il contenuto.
feature: Streaming Media
role: Developer
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 3%

---


# Fine sessione

L’evento di fine sessione chiude immediatamente e in modo irreversibile una sessione di tracciamento dei contenuti multimediali. La fine della sessione è una chiusura difficile: una volta inviata, la sessione viene terminata e non è possibile tracciare ulteriori eventi al suo interno. Utilizza Session end (Fine sessione) solo quando sei certo che non seguiranno altri eventi, come quando il lettore verrà distrutto o la pagina verrà scaricata. Nella maggior parte dei casi è più sicuro far scadere la sessione naturalmente, piuttosto che rischiare di tagliare gli eventi che potrebbero ancora arrivare. Se il visualizzatore completa il contenuto, chiamare [Sessione completata](session-complete.md).

Senza una fine di sessione esplicita, una sessione si chiude automaticamente dopo 10 minuti di nessun evento o 30 minuti di nessun movimento della testina di riproduzione.

>[!NOTE]
>
>Puoi chiamare la fine della sessione più di una volta per la stessa sessione. Il backend chiude la sessione sul primo evento e rilascia silenziosamente tutti gli eventi successivi per tale ID sessione, inclusa una seconda fine sessione. Non è necessario proteggersi da chiamate duplicate in condizioni di gara, come un timeout di 30 minuti che scade nello stesso momento in cui il visualizzatore chiude il lettore.

* **Prerequisiti**: [Inizio sessione](session-start.md)
* **Metrica associata**: nessuna

## Web SDK

Chiama [`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/sendevent/overview) con `eventType: "media.sessionEnd"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionEnd",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## Mobile SDK

Chiamare `trackSessionEnd` quando il visualizzatore chiude il lettore o si sposta.

**iOS (Swift)**

```swift
tracker.trackSessionEnd()
```

**Android (Cotlino)**

```kotlin
tracker.trackSessionEnd()
```

## Roku (BrightScript)

Chiama `sendMediaEvent` con `eventType: "media.sessionEnd"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionEnd",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [sessionEnd](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionend):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionEnd?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionEnd",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

Chiamare `trackSessionEnd` quando il visualizzatore chiude il lettore o si sposta:

```javascript
tracker.trackSessionEnd();
```

## API Media Collection

Invia un POST `sessionEnd` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "sessionEnd"
}
```
