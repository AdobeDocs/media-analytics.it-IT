---
title: Avvio annuncio
description: Conta ogni annuncio che ha iniziato a essere riprodotto durante una sessione.
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
source-wordcount: '124'
ht-degree: 12%
---

# Avvio annuncio

La metrica **Inizio annuncio** conta tutti gli annunci che hanno iniziato a essere riprodotti durante una sessione. Associalo a [Annunci completati](ad-completes.md) per calcolare il tasso di completamento degli annunci e a [Conteggio annunci](/help/reporting/metrics/ad-count.md) per il rollup equivalente a livello di sessione.

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag quando viene ricevuto un evento [ad start](/help/implementation/events/ads/ad-start.md). La metrica viene segnalata nella chiamata di inizio annuncio.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.view` quando [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.isStarted`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.ad.view` |
