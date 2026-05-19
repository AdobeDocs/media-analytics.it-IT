---
title: Tempo trascorso dell’annuncio
description: Segnala i secondi totali di riproduzione attiva dell’annuncio per sessione.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 8%

---


# Tempo trascorso dell’annuncio

La metrica **Tempo trascorso** dell&#39;annuncio indica il totale dei secondi di riproduzione attiva dell&#39;annuncio per sessione, escluse pause, buffering e blocchi. Associalo a [Tempo contenuto trascorso](/help/reporting/metrics/content-time-spent.md) per confrontare il caricamento dell&#39;annuncio con il coinvolgimento contenuto.

## Come è calcolata questa metrica

Il backend multimediale somma il tempo wall-clock trascorso tra gli eventi mentre il lettore si trova nello stato `play` su un annuncio. Il tempo durante le pause, il buffering e le ricerche è escluso, coerentemente con il modo in cui [Tempo contenuto trascorso](/help/reporting/metrics/content-time-spent.md) viene calcolato per il contenuto principale. La metrica viene segnalata nella chiamata di chiusura dell’annuncio. Il valore viene visualizzato come `HH:MM:SS` in Analysis Workspace e in secondi in Feed dati, Data Warehouse e API di reporting.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.timePlayed` quando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.timePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.ad.timePlayed` |
