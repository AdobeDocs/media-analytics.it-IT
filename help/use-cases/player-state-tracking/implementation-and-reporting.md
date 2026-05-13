---
title: Implementazione e reporting
description: Scopri come implementare la funzione di tracciamento dello stato del lettore, tra cui
exl-id: 19a97c9b-14d1-4f11-bb0a-3a1ad6f949da
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/NzekVHZYctiEjAWDpRhIdiw74amAX3wTX-z2nZDgvIw
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffacid: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 308
ht-degree: 76%

---

# Implementazione e reporting

Durante una sessione di riproduzione, ogni occorrenza di uno stato (dall’inizio alla fine) deve essere tracciata singolarmente. Media SDK e l’API Media Collection forniscono metodi di tracciamento per questa funzionalità.

Media SDK include due metodi per il tracciamento personalizzato dello stato:

`trackStateStart("state_name")`

`trackStateClose("state_name")`


L&#39;API Media Collection include due eventi che hanno `media.stateName` come parametro richiesto:

`stateStart` e `stateEnd`

## Implementazione di Media SDK

Avvio stato lettore

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


## Implementazione API Media Collection

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

## Metriche di stato

Le metriche fornite per ogni singolo stato vengono calcolate e inviate ad Adobe Analytics come parametri di dati contestuali e memorizzate a scopo di reporting. Sono disponibili tre metriche per ogni stato:

* `a.media.states.[state.name].set = true` — Imposta su true se lo stato è stato impostato almeno una volta per ogni specifica riproduzione di un flusso.
* `a.media.states.[state.name].count = 4` — Identifica il numero di occorrenze di uno stato durante ogni singola riproduzione di un flusso
* `a.media.states.[state.name].time = 240` — Identifica la durata totale dello stato in secondi per ogni singola riproduzione di un flusso

## Reporting

Tutte le metriche dello stato del lettore possono essere utilizzate per qualsiasi visualizzazione di reporting disponibile in Analysis Workspace o in un componente (segmento, metriche calcolate) una volta che una suite di rapporti è abilitata per il tracciamento dello stato del lettore. Queste metriche possono essere abilitate da Admin Console per ogni singolo rapporto utilizzando la configurazione di Media Reporting (Modifica impostazioni > Gestione file multimediali > Media Reporting).

![](assets/report-setup.png)

In Analysis Workspace, tutte le nuove proprietà si trovano nel pannello metriche. Ad esempio, puoi eseguire ricerche per `full screen` per visualizzare i dati a schermo intero nel pannello metriche.

![](assets/full-screen-report.png)

## Importazione delle metriche dichiarate del lettore in Adobe Experience Platform

I dati memorizzati in Analytics possono essere utilizzati per qualsiasi scopo e le metriche dello stato del lettore possono essere importate in Adobe Experience Platform utilizzando XDM e utilizzate con Customer Journey Analytics. Le proprietà dello stato standard hanno proprietà specifiche, mentre gli stati personalizzati sono proprietà disponibili utilizzando gli eventi personalizzati.
