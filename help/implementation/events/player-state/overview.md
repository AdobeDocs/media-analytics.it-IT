---
title: Tracciare gli stati del lettore
description: Scopri gli eventi dello stato del lettore e come tenere traccia degli stati a schermo intero, muto, sottotitoli, immagine nell’immagine e messa a fuoco.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 12%

---


# Tracciare gli stati del lettore

Gli eventi di stato del lettore tengono traccia di come i visualizzatori interagiscono con i controlli del lettore durante una sessione. Sono facoltativi e non sono richiesti per le implementazioni di tracciamento dei contenuti multimediali di base. I cinque stati tracciabili sono: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` e `inFocus`.

Gli eventi di stato del lettore sono utili per comprendere l’utilizzo della funzione di accessibilità, ad esempio la frequenza con cui i visualizzatori abilitano i sottotitoli o la disattivazione dell’audio. Rivelano inoltre pattern di visualizzazione come la visualizzazione a schermo intero o in linea e il multitasking &quot;picture-in-picture&quot;.

## Eventi del lettore

| Evento lettore | Azione |
| --- | --- |
| Il lettore entra in uno stato | Avvio stato chiamata |
| Il lettore esce da uno stato | Fine stato chiamata |

## Stati standard e personalizzati

Sono disponibili cinque stati del lettore standard e puoi aggiungere stati personalizzati.

| Nome dello stato standard | Costante Media SDK | Nome dell’API di raccolta multimediale |
|----|----|----|
| A schermo intero | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Sottotitoli codificati | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Disattiva audio | `ADB.Media.PlayerState.Mute` | `mute` |
| Immagine nell’immagine | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| In focus | `ADB.Media.PlayerState.InFocus` | `inFocus` |

Consulta [Variabili di stato del lettore](/help/implementation/variables/player-state/) per il riferimento completo alle variabili, inclusi i percorsi XDM e le definizioni delle metriche.

**Stati personalizzati:** Puoi creare stati personalizzati per acquisire comportamenti aggiuntivi del lettore specifici dell&#39;applicazione. Per informazioni dettagliate sulla creazione di oggetti stato personalizzati, vedere il riferimento all&#39;API [Media: `createStateObject`](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/).

## Passaggi di implementazione

1. **Chiama [Avvio stato](state-start.md)** quando il lettore entra in uno dei cinque stati tracciabili. Più stati possono essere attivi contemporaneamente e più stati possono essere avviati nella stessa chiamata evento.
1. **Chiama [Stato fine](state-end.md)** quando il lettore esce da uno stato. Più stati possono terminare nella stessa chiamata dell’evento, e gli stati possono essere avviati e terminati insieme in una singola chiamata.

## Linee guida

* Una sessione video è limitata a 10 stati del lettore.
* È consentita qualsiasi combinazione di stati.
* Se vengono passati più stati del lettore, solo i primi 10 vengono mantenuti e inoltrati a valle al backend multimediale.
* Il massimo di 10 stati si applica a tutti gli stati, indipendentemente dal fatto che siano aperti o chiusi.
* Uno stato può iniziare e terminare più volte e conta come un singolo stato. Ad esempio, `closedCaptioning` può essere avviato e arrestato cinque volte, ma conta come un unico stato.
* Lo stato del lettore viene calcolato in tutti gli stati di riproduzione (senza suddivisione).
* Gli stati del lettore vengono acquisiti per ogni singola sessione di riproduzione. Lo stato del lettore non viene calcolato tra le riproduzioni.
* La conoscenza dello stato dell’applicazione non viene mantenuta dopo l’arresto di uno stato. Al termine di uno stato, è necessario riavviarlo per continuare il tracciamento.

## Aggiornamento simultaneo di più stati

Sulle piattaforme basate su XDM, è possibile eseguire il batch di più modifiche di stato in una singola chiamata `statesUpdate` utilizzando gli array in `statesStart` e `statesEnd`. Sugli SDK per dispositivi mobili, ogni modifica dello stato richiede una chiamata separata.

Gli esempi seguenti iniziano a disattivare l’audio e a inserire un’immagine nell’immagine insieme, quindi passano alla modalità a schermo intero.

## Tipi di implementazione consigliati

>[!BEGINTABS]

>[!TAB Web SDK]

```javascript
// t0 — start mute and picture-in-picture together
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }, { name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t1 — end mute and picture-in-picture; start full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "mute" }, { name: "pictureInPicture" }],
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t2 — end full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Mobile SDK non supporta la gestione in batch: invia una chiamata separata per ogni modifica dello stato.

```swift
// t0 — start mute and picture-in-picture
let muteState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.MUTE)
let pipState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(event: MediaEvent.StateStart, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateStart, info: pipState, metadata: nil)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateEnd, info: pipState, metadata: nil)
let fullscreenState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(event: MediaEvent.StateStart, info: fullscreenState, metadata: nil)

// t2 — end full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: fullscreenState, metadata: nil)
```

>[!TAB Android]

Mobile SDK non supporta la gestione in batch: invia una chiamata separata per ogni modifica dello stato.

```kotlin
// t0 — start mute and picture-in-picture
val muteState = Media.createStateObject(MediaConstants.PlayerState.MUTE)
val pipState = Media.createStateObject(MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(Media.Event.StateStart, muteState, null)
tracker.trackEvent(Media.Event.StateStart, pipState, null)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(Media.Event.StateEnd, muteState, null)
tracker.trackEvent(Media.Event.StateEnd, pipState, null)
val fullscreenState = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(Media.Event.StateStart, fullscreenState, null)

// t2 — end full screen
tracker.trackEvent(Media.Event.StateEnd, fullscreenState, null)
```

>[!TAB Roku]

```brightscript
' t0 — start mute and picture-in-picture together
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "playhead": 0
        }
    }
})

' t1 — end mute and picture-in-picture; start full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "statesStart": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})

' t2 — end full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})
```

>[!TAB API Media Edge]

```sh
# t0 — start mute and picture-in-picture together
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:00:00+00:00"
    }
  }]
}'

# t1 — end mute and picture-in-picture; start full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "statesStart": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:01:00+00:00"
    }
  }]
}'

# t2 — end full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:02:00+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## Tipi di implementazione legacy (solo Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Più modifiche dello stato richiedono chiamate separate.

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
var pipState = ADB.Media.createStateObject(ADB.Media.PlayerState.PictureInPicture);
tracker.trackPlayerStateStart(muteState);
tracker.trackPlayerStateStart(pipState);

// t1 — end mute and picture-in-picture; start full screen
tracker.trackPlayerStateEnd(muteState);
tracker.trackPlayerStateEnd(pipState);
var fullscreenState = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);
tracker.trackPlayerStateStart(fullscreenState);

// t2 — end full screen
tracker.trackPlayerStateEnd(fullscreenState);
```

>[!TAB Chromecast]

Più modifiche dello stato richiedono chiamate separate.

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.Mute);
var pipState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.PictureInPicture);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, pipState, null);

// t1 — end mute and picture-in-picture; start full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, pipState, null);
var fullscreenState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, fullscreenState, null);

// t2 — end full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, fullscreenState, null);
```

>[!TAB API Media Collection]

```json
// t0 — start mute and picture-in-picture together
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999130627 }
}

// t1 — end mute and picture-in-picture; start full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ],
    "statesStart": [
      { "media.state.name": "fullScreen" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999230627 }
}

// t2 — end full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [{ "media.state.name": "fullScreen" }]
  },
  "playerTime": { "playhead": 0, "ts": 1569999330627 }
}
```

>[!ENDTABS]

## Pausa lunga

Quando una sessione video ha una pausa di durata superiore a 30 minuti, l’API richiede una nuova sessione. Genera un nuovo ID sessione e mantieni tutti gli stati attivi in modo che possano essere ripristinati con `stateStart` eventi subito dopo la nuova chiamata `sessionStart`.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

Dopo l&#39;invio di `sessionEnd`, avviare una nuova sessione e inviare nuovamente immediatamente gli stati attivi:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

## Metriche dello stato

Vengono calcolate tre metriche per ogni stato tracciato e inviato ad Adobe Analytics nella chiamata di chiusura dei contenuti multimediali:

| Metrica | Chiave dati contestuali | Descrizione |
| --- | --- | --- |
| Stato impostato | `a.media.states.[state.name].set = true` | `true` se lo stato è stato impostato almeno una volta durante la riproduzione |
| Conteggio stati | `a.media.states.[state.name].count = 4` | Numero di volte in cui si è verificato lo stato durante la riproduzione |
| Ora stato | `a.media.states.[state.name].time = 240` | Tempo totale (secondi) trascorso nello stato durante la riproduzione |
