---
title: Completamenti del capitolo
description: Conta ogni capitolo riprodotto fino al completamento.
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
source-wordcount: '121'
ht-degree: 12%
---

# Completamenti del capitolo

La metrica **Chapter completes** conta ogni capitolo riprodotto fino al completamento. Associalo a [Inizio capitolo](chapter-starts.md) per calcolare il tasso di completamento del capitolo.

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag quando viene ricevuto un evento [chapter complete](/help/implementation/events/chapters/chapter-complete.md). La metrica viene segnalata nella chiamata di chiusura del capitolo. I capitoli saltati o abbandonati nel mid-play non vengono considerati completamenti.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.chapter.complete` quando [[!UICONTROL Media Chapters]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.isCompleted`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.chapter.complete` |
