---
title: Avvio annuncio
description: Conta ogni annuncio che ha iniziato a essere riprodotto durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 12%

---


# Avvio annuncio

La metrica **Inizio annuncio** conta tutti gli annunci che hanno iniziato a essere riprodotti durante una sessione. Associalo a [Annunci completati](ad-completes.md) per calcolare il tasso di completamento degli annunci e a [Conteggio annunci](/help/reporting/metrics/ad-count.md) per il rollup equivalente a livello di sessione.

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag quando viene ricevuto un evento [ad start](/help/implementation/events/ads/ad-start.md). La metrica viene segnalata nella chiamata di inizio annuncio.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.view` quando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.ad.view` |
