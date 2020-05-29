---
title: Implementazione e generazione dei rapporti
description: Questo argomento descrive come implementare la funzione di tracciamento dello stato del lettore, inclusa .
translation-type: tm+mt
source-git-commit: 1b48565bcc5c9a87e5fabbc906049ab791bf89cc
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---


# Implementazione e reporting

Durante una sessione di riproduzione, ogni occorrenza di stato (dall’inizio alla fine) deve essere tracciata singolarmente. L’SDK per file multimediali e l’API per la raccolta di file multimediali forniscono nuovi metodi di tracciamento per questa funzionalità.

Media SDK include due nuovi metodi per il tracciamento dello stato personalizzato:

`trackStateStart("state_name")`

`trackStateClose("state_name")`


L&#39;API Media Collection include due nuovi eventi che hanno `media.stateName` come parametro richiesto:

`stateStart` (Componenti di progetto non curati) e `stateEnd` (Componenti VRS non curati)

## Implementazione di Media SDK

Stato del lettore

```
// StateStart (ex: Mute is switched on)
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);
```

Fine stato lettore

```
// StateEnd (ex: Mute is switched off)
tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```


## Implementazione API di Media Collection

Stato del lettore

```
// StateStart (ex: Mute is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

Fine stato lettore

```
// StateEnd (ex: Mute is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events

{
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 600,
    "ts": 1569999730638
  }
}
```

## Metriche stato

Le metriche fornite per ogni singolo stato vengono calcolate e inviate ad Adobe Analytics come parametri di dati contestuali e memorizzate a scopo di reporting. Sono disponibili tre metriche per ogni stato:

* `a.media.states.[state.name].set = true` — Impostato su true se lo stato è stato impostato almeno una volta per ogni specifica riproduzione di un flusso.
* `a.media.states.[state.name].count = 4` — Identifica il numero di occorrenze di uno stato durante ogni singola riproduzione di un flusso
* `a.media.states.[state.name].time = 240` — Identifica la durata totale dello stato in secondi per ogni singola riproduzione di un flusso

## Generazione di rapporti

Tutte le metriche dello stato del lettore possono essere utilizzate per qualsiasi visualizzazione di reporting disponibile in Analysis Workspace o in un componente (segmenti, metriche calcolate) una volta che una suite di rapporti è abilitata per il tracciamento dello stato del lettore. Le nuove metriche possono essere attivate dall’Admin Console per ogni singolo rapporto utilizzando Configurazione Media Reporting (Modifica impostazioni > Gestione file multimediali > Generazione rapporti multimediali).

![](assets/report-setup.png)

In Analytics Workspace, tutte le nuove proprietà si trovano nel pannello delle metriche. Ad esempio, puoi eseguire una ricerca per `full screen` visualizzare i dati a schermo intero nel pannello delle metriche.

![](assets/full-screen-report.png)

## Importazione di metriche del lettore dichiarate in Adobe Experience Platform

I dati memorizzati in Analytics possono essere utilizzati per qualsiasi scopo e le metriche dello stato del lettore possono essere importate in Adobe Experience Platform utilizzando XDM e utilizzate con Customer Journey Analytics. Le proprietà dello stato standard hanno proprietà specifiche, mentre gli stati personalizzati sono proprietà disponibili tramite gli eventi personalizzati. Per ulteriori informazioni sulle proprietà standard dello stato, consultate la sezione *Proprietà elenco per identità* XDM nella pagina Parametri [dello stato del](/help/metrics-and-metadata/player-state-parameters.md) lettore.
