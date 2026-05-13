---
title: Inizio capitolo
description: Conta ogni capitolo che ha iniziato a essere riprodotto durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 12%

---


# Inizio capitolo

La metrica **Inizio capitolo** conta tutti i capitoli che hanno iniziato la riproduzione durante una sessione. Associalo a [Completamenti del capitolo](chapter-completes.md) per calcolare il tasso di completamento del capitolo.

## Come è calcolata questa metrica

Il backend multimediale imposta `mediaReporting.chapterDetails.isStarted = true` quando viene ricevuto un evento `media.chapterStart`. La metrica viene segnalata nella chiamata di chiusura del capitolo.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.chapter.view` quando [[!UICONTROL Media Chapters]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
