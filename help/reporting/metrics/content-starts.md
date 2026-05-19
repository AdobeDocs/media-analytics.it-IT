---
title: Inizio contenuto
description: Conta le sessioni in cui il contenuto principale ha effettivamente iniziato a essere riprodotto.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.play` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isPlayed`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.play` |
