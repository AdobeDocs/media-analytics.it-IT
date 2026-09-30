---
title: Inizio contenuto
description: Conta le sessioni in cui il contenuto principale ha effettivamente iniziato a essere riprodotto.
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
source-wordcount: '146'
ht-degree: 10%
---

# Inizio contenuto

La metrica **Avvio del contenuto** conta le sessioni in cui il contenuto principale ha effettivamente iniziato la riproduzione. A differenza di [Media starts](media-starts.md), sono escluse le sessioni terminate durante annunci pre-roll, buffering o blocchi. Questo lo rende il denominatore giusto per i tassi di completamento e di coinvolgimento.

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag la prima volta che viene ricevuto un evento [play](/help/implementation/events/playback/play.md) per il contenuto principale. La metrica viene attivata su tale evento di riproduzione, ma viene segnalata sulla chiamata di chiusura. Per calcolare la velocità di rilascio pre-roll, utilizzare `(Media starts − Content starts) / Media starts`.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.play` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isPlayed`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.play` |
