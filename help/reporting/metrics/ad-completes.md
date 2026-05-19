---
title: Annuncio completato
description: Conta ogni annuncio riprodotto fino al completamento.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 12%

---


# Annuncio completato

La metrica **Annuncio completato** conta ogni annuncio riprodotto fino al completamento. Associalo a [Inizio annuncio](ad-starts.md) per calcolare il tasso di completamento dell&#39;annuncio.

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag quando viene ricevuto un evento [ad complete](/help/implementation/events/ads/ad-complete.md). La metrica viene segnalata nella chiamata di chiusura dell’annuncio. Gli annunci saltati o abbandonati non vengono conteggiati come completamenti.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.complete` quando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.isCompleted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.ad.complete` |
