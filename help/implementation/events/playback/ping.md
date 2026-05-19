---
title: Ping
description: Invia un heartbeat per mantenere attiva la sessione multimediale e tenere traccia dell’avanzamento della riproduzione a intervalli regolari.
feature: Streaming Media
role: Developer
source-git-commit: 6534e4c76dcb4113bbbb99aed2a0e350f9256b15
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 4%

---


# Ping

L’evento ping è un heartbeat che mantiene attiva la sessione e tiene traccia dell’avanzamento della riproduzione. Inviarla con un timer durante la riproduzione. Sugli SDK per dispositivi mobili, i ping vengono inviati automaticamente; su tutte le altre piattaforme devono essere inviati manualmente nell’intervallo specificato.

* **Contenuto principale**: primo ping 10 secondi dopo l&#39;avvio della riproduzione, quindi ogni 10 secondi
* **Contenuto annuncio**: ogni 1 secondo durante il tracciamento degli annunci

Non includere un oggetto `params` nel corpo della richiesta ping.

* **Prerequisiti**: [Inizio sessione](../session/session-start.md)
* **Metrica associata**: nessuna

## Web SDK

Pianifica una chiamata `sendEvent` ricorrente con `eventType: "media.ping"`. Aggiorna `playhead` alla posizione di riproduzione corrente in ogni chiamata:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.ping",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 10
    }
  }
});
```

## Mobile SDK

Il SDK mobile invia automaticamente gli eventi ping. Non è richiesta alcuna chiamata esplicita.

## Roku (BrightScript)

Pianifica una chiamata `sendMediaEvent` ricorrente con `eventType: "media.ping"`. Aggiorna `playhead` alla posizione di riproduzione corrente in ogni chiamata:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.ping",
        "mediaCollection": {
            "playhead": 10
        }
    }
})
```

## API di Media Edge

Chiama l&#39;endpoint [ping](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ping/) in un timer. Adobe consiglia di eseguire il primo ping 10 secondi dopo l’inizio della riproduzione principale, ogni 10 secondi dopo tale inizio e ogni 1 secondo durante il tracciamento degli annunci:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/ping?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.ping",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 10
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## Media SDK

Media SDK invia automaticamente gli eventi ping. Non è richiesta alcuna chiamata esplicita.

## API Media Collection

Invia un POST `ping` all&#39;endpoint [eventi](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) in un timer. Non includere un oggetto `params`:

```json
{
  "playerTime": { "playhead": 10, "ts": 1699523820000 },
  "eventType": "ping"
}
```
