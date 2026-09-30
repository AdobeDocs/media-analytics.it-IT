---
title: Tempo trascorso dell’annuncio
description: Segnala i secondi totali di riproduzione attiva dell’annuncio per sessione.
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
source-wordcount: '172'
ht-degree: 8%
---

# Tempo trascorso dell’annuncio

La metrica **Tempo trascorso** dell&#39;annuncio indica il totale dei secondi di riproduzione attiva dell&#39;annuncio per sessione, escluse pause, buffering e blocchi. Associalo a [Tempo contenuto trascorso](/help/reporting/metrics/content-time-spent.md) per confrontare il caricamento dell&#39;annuncio con il coinvolgimento contenuto.

## Come è calcolata questa metrica

Il backend multimediale somma il tempo wall-clock trascorso tra gli eventi mentre il lettore si trova nello stato `play` su un annuncio. Il tempo durante le pause, il buffering e le ricerche è escluso, coerentemente con il modo in cui [Tempo contenuto trascorso](/help/reporting/metrics/content-time-spent.md) viene calcolato per il contenuto principale. La metrica viene segnalata nella chiamata di chiusura dell’annuncio. Il valore viene visualizzato come `HH:MM:SS` in Analysis Workspace e in secondi in Feed dati, Data Warehouse e API di reporting.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.timePlayed` quando [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.timePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.ad.timePlayed` |
