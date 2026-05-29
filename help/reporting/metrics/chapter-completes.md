---
title: Completamenti del capitolo
description: Conta ogni capitolo riprodotto fino al completamento.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.chapter.complete` quando [[!UICONTROL Media Chapters]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.isCompleted`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.chapter.complete` |
