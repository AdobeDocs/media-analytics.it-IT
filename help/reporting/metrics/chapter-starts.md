---
title: Inizio capitolo
description: Conta ogni capitolo che ha iniziato a essere riprodotto durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 13%

---


# Inizio capitolo

La metrica **Inizio capitolo** conta tutti i capitoli che hanno iniziato la riproduzione durante una sessione. Associalo a [Completamenti del capitolo](chapter-completes.md) per calcolare il tasso di completamento del capitolo.

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag quando viene ricevuto un evento [chapter start](/help/implementation/events/chapters/chapter-start.md). La metrica viene segnalata nella chiamata di chiusura del capitolo.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.chapter.view` quando [[!UICONTROL Media Chapters]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.chapter.view` |
