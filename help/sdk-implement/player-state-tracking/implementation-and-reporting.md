---
title: Implementazione e reporting
description: Scopri come implementare la funzione di tracciamento dello stato del lettore, tra cui .
exl-id: 19a97c9b-14d1-4f11-bb0a-3a1ad6f949da
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 2%

---

# Implementazione e reporting

Durante una sessione di riproduzione, ogni occorrenza dello stato (dall’inizio alla fine) deve essere tracciata singolarmente. Media SDK e API di raccolta multimediale forniscono nuovi metodi di tracciamento per questa funzionalità.

Media SDK include due nuovi metodi per il tracciamento dello stato personalizzato:

`trackStateStart("state_name")`

`trackStateClose("state_name")`


L’API di raccolta multimediale include due nuovi eventi con `media.stateName` come parametro richiesto:

`stateStart` e `stateEnd`

## Implementazione Media SDK

Avvio stato lettore

```
// StateStart (ex: Mute is switched on)
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);
```

Lo Stato Del Lettore Termina

```
// StateEnd (ex: Mute is switched off)
tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```


## Implementazione API di Media Collection

Avvio stato lettore

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

Lo Stato Del Lettore Termina

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

## Metriche di stato

Le metriche fornite per ogni singolo stato vengono calcolate e inviate ad Adobe Analytics come parametri di dati contestuali e memorizzate a scopo di reporting. Sono disponibili tre metriche per ogni stato:

* `a.media.states.[state.name].set = true` — Impostare su true se lo stato è stato impostato almeno una volta per ogni specifica riproduzione di un flusso.
* `a.media.states.[state.name].count = 4` — Identifica il numero di occorrenze di uno stato durante ogni singola riproduzione di un flusso
* `a.media.states.[state.name].time = 240` — Identifica la durata totale dello stato in secondi per ogni singola riproduzione di un flusso

## Generazione di rapporti

Tutte le metriche dello stato del lettore possono essere utilizzate per qualsiasi visualizzazione di reporting disponibile in Analysis Workspace o in un componente (segmento, metriche calcolate) una volta che una suite di rapporti è abilitata per il tracciamento dello stato del lettore. Le nuove metriche possono essere abilitate nell’Admin Console per ogni singolo rapporto utilizzando Media Reporting Setup (Modifica impostazioni > Media Management > Media Reporting).

![](assets/report-setup.png)

In Analysis Workspace, tutte le nuove proprietà si trovano nel pannello metriche . Ad esempio, puoi eseguire una ricerca per `full screen` per visualizzare i dati a schermo intero nel pannello metriche.

![](assets/full-screen-report.png)

## Importazione delle metriche dichiarate del lettore in Adobe Experience Platform

I dati memorizzati in Analytics possono essere utilizzati per qualsiasi scopo e le metriche dello stato del lettore possono essere importate in Adobe Experience Platform utilizzando XDM e utilizzate con il Customer Journey Analytics. Le proprietà dello stato standard hanno proprietà specifiche, mentre gli stati personalizzati sono proprietà disponibili utilizzando gli eventi personalizzati. Per ulteriori informazioni sulle proprietà dello stato standard, consulta la sezione *Elenco proprietà per le identità XDM* nella pagina [Parametri dello stato del lettore](/help/metrics-and-metadata/player-state-parameters.md) .
