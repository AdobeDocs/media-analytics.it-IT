---
title: Tempo trascorso dei contenuti multimediali
description: Segnala i secondi totali di riproduzione attiva per sessione, inclusi gli annunci.
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
source-wordcount: '180'
ht-degree: 8%
---

# Tempo trascorso dei contenuti multimediali

La metrica **Tempo trascorso** per contenuti multimediali indica i secondi totali di riproduzione attiva per sessione, inclusi sia il contenuto principale che gli annunci ma escluse pause, buffering e blocchi. Utilizzalo per misurare il tempo totale in cui il visualizzatore è stato attivamente coinvolto con il lettore. Solo per il contenuto principale, utilizza [Tempo contenuto trascorso](content-time-spent.md).

## Come è calcolata questa metrica

Il backend multimediale somma il tempo wall-clock trascorso tra gli eventi mentre il lettore è nello stato `play`, sul contenuto principale o sugli annunci. È escluso il tempo durante pause, eventi buffer e blocchi. La metrica viene segnalata nella chiamata di chiusura. Il valore viene visualizzato come `HH:MM:SS` in Analysis Workspace e in secondi in Feed dati, Data Warehouse e API di reporting.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.totalTimePlayed` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.totalTimePlayed`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.totalTimePlayed` |
