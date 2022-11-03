---
title: Aggiornamento simultaneo di più stati del lettore
description: Questo argomento descrive la funzione di tracciamento di più stati del lettore.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: fdbb777547181422b81ff6f7874bec3d317d02e9
workflow-type: ht
source-wordcount: '186'
ht-degree: 100%

---

# Tracciamento di più stati del lettore

A volte due stati del lettore iniziano e terminano contemporaneamente oppure il termine di uno stato è anche l’inizio di un altro, come mostrato nell’immagine seguente:

![Più stati del lettore](assets/multiple-player-states.svg)

L’implementazione corrente consente di eseguire entrambe gli scenari:
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

Tuttavia, questo richiede di emettere più eventi `stateStart` e `stateEnd` per segnalare più modifiche simultanee dello stato. Per
ottimizzare questo comportamento comune, è stato implementato un nuovo tipo di evento `statesUpdate`, che termina un elenco di stati
e ne avvia uno di nuovi stati.

Utilizzando il nuovo evento `statesUpdate`, l’elenco di eventi precedente diventa:
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

Il numero di chiamate per gli aggiornamenti di stato è stato ridotto da sei a tre per lo stesso comportamento. L’ultimo evento
avrebbe potuto essere anche un semplice `stateEnd(fullScreen)`.

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
