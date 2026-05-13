---
source-git-commit: c06ecd16f417c9584fb87181074d1c2bee487e0b
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 5%

---
﻿---
title: Metriche calcolate
description: Metriche calcolate personalizzate per il reporting di contenuti multimediali in streaming in Adobe Analytics e Customer Journey Analytics.
feature: Metrics
role: User, Admin
---

# Metriche calcolate

Le metriche calcolate per i servizi di contenuti multimediali in streaming di Adobe sono metriche personalizzate basate sulle metriche dei contenuti multimediali in streaming standard, che consentono di ottenere rapporti quali il tempo medio trascorso o il tasso di completamento dei contenuti multimediali senza modificare l’implementazione.

Per creare queste metriche calcolate in Analysis Workspace, vedi la panoramica delle rispettive metriche calcolate in [Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/components/calculated-metrics/cm-overview) o [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview).

| Metrica calcolata | Descrizione | Formula |
| --- | --- | --- |
| Media annunci per flusso multimediale | Avvio annuncio per avvio file multimediali | [`Ad Starts`](/help/reporting/metrics/ad-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Media capitoli per flusso multimediale | Avvio del capitolo per avvio del contenuto multimediale | [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Media tempo trascorso dei contenuti multimediali | Tempo totale trascorso per avvio file multimediali (`HH:MM:SS`) | [`Media Time Spent`](/help/reporting/metrics/media-time-spent.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Media tempo trascorso dei contenuti | Tempo trascorso contenuto per avvio contenuto (`HH:MM:SS`) | [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| Media tempo trascorso dell’annuncio | Tempo trascorso annuncio per avvio annuncio (`HH:MM:SS`) | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| Media tempo trascorso capitolo | Tempo trascorso capitolo per avvio capitolo (`HH:MM:SS`) | [`Chapter Time Spent`](/help/reporting/metrics/chapter-time-spent.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| Percentuale di completamento file multimediali | Percentuale di completamento dei contenuti rispetto ai contenuti multimediali avviati | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Percentuale di completamento dei contenuti | Percentuale di completamento dei contenuti rispetto all&#39;avvio dei contenuti | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| Percentuale di completamento degli annunci | Percentuale di completamenti e avvii degli annunci | [`Ad Completes`](/help/reporting/metrics/ad-completes.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| Tasso di completamento capitolo | Percentuale di completamento del capitolo rispetto all’inizio del capitolo | [`Chapter Completes`](/help/reporting/metrics/chapter-completes.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| Perdita prima della frequenza di avvio | Percentuale di cadute prima dell’avvio rispetto all’avvio del contenuto multimediale | [`Drops Before Start`](/help/reporting/metrics/drops-before-start.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Percentuale durata pausa contenuti | Percentuale di durata totale della pausa rispetto al tempo trascorso dei contenuti | [`Total Pause Duration`](/help/reporting/metrics/total-pause-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| Percentuale durata buffer dei contenuti | Percentuale di durata totale del buffer rispetto al tempo trascorso dei contenuti | [`Total Buffer Duration`](/help/reporting/metrics/total-buffer-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| Percentuale tempo di avvio dei contenuti | Percentuale di tempo di avvio rispetto al tempo trascorso dei contenuti | [`Time to Start`](/help/reporting/metrics/time-to-start.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| Percentuale tempo trascorso dell’annuncio | Percentuale di tempo trascorso degli annunci rispetto al tempo trascorso dei contenuti | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
