---
title: Aggiornamento simultaneo di più stati del lettore
description: Questo argomento descrive la funzione di tracciamento di più stati del lettore.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 7a512a81-a6d1-4d0c-a4fe-91e9b11419db
TQID: https://experienceleague.adobe.com/fKpr-TULVqDnK7j07e66gd-kiFLYzf7D2GmoGtP8Aqg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 186
ht-degree: 80%

---

# Tracciamento di più stati del lettore

A volte due stati del lettore iniziano e terminano contemporaneamente oppure il termine di uno stato è anche l’inizio di un altro, come mostrato nell’immagine seguente:

![Più stati del lettore](assets/multiple-player-states.png)

L’implementazione corrente consente di eseguire entrambe gli scenari:
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

Tuttavia, questo richiede di emettere più eventi `stateStart` e `stateEnd` per segnalare più modifiche simultanee dello stato. In entrata
per ottimizzare questo comportamento comune, è stato implementato un nuovo tipo di evento `statesUpdate`, che termina un elenco di stati
e avvia un elenco di nuovi stati.

Utilizzando il nuovo evento `statesUpdate`, l’elenco di eventi precedente diventa:
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

Il numero di chiamate per gli aggiornamenti di stato è stato ridotto da sei a tre per lo stesso comportamento. L’ultimo evento
potrebbe essere stato anche un `stateEnd(fullScreen)` semplice.

## Implementazione API Media Collection {#mpst-api}

Puoi utilizzare l’API Media Collection per implementare il tracciamento di più stati del lettore.

### Esempio

Di seguito è riportato un esempio di implementazione dell’API Media Collection per il tracciamento di più stati del lettore.

```
// statesUpdate (ex: mute and pictureInPicture are switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: mute and pictureInPicture are switched off, fullScreen is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ],
    "statesStart": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: fullScreen is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

## Implementazione di Media SDK

Non esiste alcuna implementazione di Media SDK.
