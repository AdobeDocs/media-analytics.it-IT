---
title: Metriche calcolate
description: Metriche calcolate personalizzate per il reporting di contenuti multimediali in streaming in Adobe Analytics e Customer Journey Analytics.
feature: Metrics
role: User, Admin
source-git-commit: cb3770abd06eb8debe4ff92641835f04f62471f7
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 6%

---

# Metriche calcolate per contenuti multimediali in streaming

Le metriche calcolate per i servizi di contenuti multimediali in streaming di Adobe sono metriche personalizzate basate sulle metriche dei contenuti multimediali in streaming standard, che consentono di ottenere rapporti quali il tempo medio trascorso o il tasso di completamento dei contenuti multimediali senza modificare l’implementazione.

Per creare queste metriche calcolate in Analysis Workspace, vedi la panoramica delle rispettive metriche calcolate in [Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/components/calculated-metrics/cm-overview) o [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview).

| Metrica calcolata | Descrizione | Formula |
| --- | --- | --- |
| Media annunci per flusso multimediale | [[!UICONTROL Ad starts]](/help/reporting/metrics/ad-starts.md) per [[!UICONTROL Media starts]](/help/reporting/metrics/media-starts.md) | `[Ad starts] / [Media starts]` |
| Media capitoli per flusso multimediale | [[!UICONTROL Chapter starts]](/help/reporting/metrics/chapter-starts.md) per [[!UICONTROL Media starts]](/help/reporting/metrics/media-starts.md) | `[Chapter starts] / [Media starts]` |
| Media tempo trascorso dei contenuti multimediali | [[!UICONTROL Media time spent]](/help/reporting/metrics/media-time-spent.md) per [[!UICONTROL Media starts]](/help/reporting/metrics/media-starts.md) (`HH:MM:SS`) | `[Media time spent] / [Media starts]` |
| Media tempo trascorso dei contenuti | [[!UICONTROL Content time spent]](/help/reporting/metrics/content-time-spent.md) per [[!UICONTROL Content starts]](/help/reporting/metrics/content-starts.md) (`HH:MM:SS`) | `[Content time spent] / [Content starts]` |
| Media tempo trascorso dell’annuncio | [[!UICONTROL Ad time spent]](/help/reporting/metrics/ad-time-spent.md) per [[!UICONTROL Ad starts]](/help/reporting/metrics/ad-starts.md) (`HH:MM:SS`) | `[Ad time spent] / [Ad starts]` |
| Media tempo trascorso capitolo | [[!UICONTROL Chapter time spent]](/help/reporting/metrics/chapter-time-spent.md) per [[!UICONTROL Chapter starts]](/help/reporting/metrics/chapter-starts.md) (`HH:MM:SS`) | `[Chapter time spent] / [Chapter starts]` |
| Percentuale di completamento file multimediali | Percentuale di [[!UICONTROL Content completes]](/help/reporting/metrics/content-completes.md) rispetto a [[!UICONTROL Media starts]](/help/reporting/metrics/media-starts.md) | `[Content completes] / [Media starts]` |
| Percentuale di completamento dei contenuti | Percentuale di [[!UICONTROL Content completes]](/help/reporting/metrics/content-completes.md) rispetto a [[!UICONTROL Content starts]](/help/reporting/metrics/content-starts.md) | `[Content completes] / [Content starts]` |
| Percentuale di completamento degli annunci | Percentuale di [[!UICONTROL Ad completes]](/help/reporting/metrics/ad-completes.md) rispetto a [[!UICONTROL Ad starts]](/help/reporting/metrics/ad-starts.md) | `[Ad completes] / [Ad starts]` |
| Tasso di completamento capitolo | Percentuale di [[!UICONTROL Chapter completes]](/help/reporting/metrics/chapter-completes.md) rispetto a [[!UICONTROL Chapter starts]](/help/reporting/metrics/chapter-starts.md) | `[Chapter completes] / [Chapter starts]` |
| Perdita prima della frequenza di avvio | Percentuale di [[!UICONTROL Drops before start]](/help/reporting/metrics/drops-before-start.md) rispetto a [[!UICONTROL Media starts]](/help/reporting/metrics/media-starts.md) | `[Drops before start] / [Media starts]` |
| Percentuale durata pausa contenuti | Percentuale di [[!UICONTROL Total pause duration]](/help/reporting/metrics/total-pause-duration.md) rispetto a [[!UICONTROL Content time spent]](/help/reporting/metrics/content-time-spent.md) | `[Total pause duration] / [Content time spent]` |
| Percentuale durata buffer dei contenuti | Percentuale di [[!UICONTROL Total buffer duration]](/help/reporting/metrics/total-buffer-duration.md) rispetto a [[!UICONTROL Content time spent]](/help/reporting/metrics/content-time-spent.md) | `[Total buffer duration] / [Content time spent]` |
| Percentuale tempo di avvio dei contenuti | Percentuale di [[!UICONTROL Time to start]](/help/reporting/metrics/time-to-start.md) rispetto a [[!UICONTROL Content time spent]](/help/reporting/metrics/content-time-spent.md) | `[Time to start] / [Content time spent]` |
| Percentuale tempo trascorso dell’annuncio | Percentuale di [[!UICONTROL Ad time spent]](/help/reporting/metrics/ad-time-spent.md) rispetto a [[!UICONTROL Content time spent]](/help/reporting/metrics/content-time-spent.md) | `[Ad time spent] / [Content time spent]` |

