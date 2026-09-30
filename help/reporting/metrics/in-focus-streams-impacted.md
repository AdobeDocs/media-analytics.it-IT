---
title: Flussi interessati da in focus
description: Conta le sessioni in cui il lettore era a fuoco almeno una volta.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 8%
---

# Flussi interessati da in focus

>[!BEGINSHADEBOX]

*In questa pagina sono descritti i **Flussi interessati dalla metrica di reporting in focus**. Per informazioni su come raccogliere questa variabile, vedere [In focus](/help/implementation/variables/player-state/in-focus.md).*

>[!ENDSHADEBOX]

La metrica **Flussi interessati da in focus** conta le sessioni in cui il lettore era attivo almeno una volta. La metrica è un valore booleano a livello di sessione; più eventi di attivazione all’interno della stessa sessione vengono conteggiati come un flusso interessato. Per il volume totale degli eventi di attivazione, utilizzare [Conteggi attivazione](in-focus-count.md).

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag la prima volta che viene ricevuto un evento di avvio dello stato attivo durante la sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.states.infocus.set` quando [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | Voce [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) in cui `name = "inFocus"`, campo `isSet` |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.infocus.set` |
