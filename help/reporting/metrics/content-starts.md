---
title: Inizio contenuto
description: Conta le sessioni in cui il contenuto principale ha effettivamente iniziato a essere riprodotto.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 9%

---


# Inizio contenuto

La metrica **Avvio del contenuto** conta le sessioni in cui il contenuto principale ha effettivamente iniziato la riproduzione. A differenza di [Media starts](media-starts.md), sono escluse le sessioni terminate durante annunci pre-roll, buffering o blocchi. Questo lo rende il denominatore giusto per i tassi di completamento e di coinvolgimento.

## Come è calcolata questa metrica

Il backend multimediale imposta `mediaReporting.sessionDetails.isPlayed = true` la prima volta che viene ricevuto un evento `media.play` per il contenuto principale. La metrica viene attivata su tale evento di riproduzione, ma viene segnalata sulla chiamata di chiusura. Per calcolare la velocità di rilascio pre-roll, utilizzare `(Media starts − Content starts) / Media starts`.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.play` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isPlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
