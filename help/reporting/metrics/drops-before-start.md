---
title: Perdite prima dell’inizio
description: Conta le sessioni in cui il visualizzatore si chiude prima di eseguire il rendering di qualsiasi contenuto principale.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 8%

---


# Perdite prima dell’inizio

La metrica **Perde prima dell&#39;inizio** conta le sessioni in cui il visualizzatore si chiude prima di eseguire il rendering di qualsiasi contenuto principale. La metrica contrassegna l’abbandono pre-contenuto indipendentemente dal comportamento dell’annuncio, quindi è la migliore misura del drop-off puro pre-contenuto. Associalo a [Avvii file multimediali](/help/reporting/metrics/media-starts.md) e [Inizio contenuto](/help/reporting/metrics/content-starts.md) per calcolare la condivisione di sessioni che non hanno mai prodotto un frame di contenuto.

## Come è calcolata questa metrica

Il backend multimediale imposta `mediaReporting.qoeDataDetails.isDroppedBeforeStart = true` per le sessioni che si chiudono senza mai produrre un evento `media.play` sul contenuto principale. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.dropBeforeStart` quando [[!UICONTROL Media Quality]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.isDroppedBeforeStart`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
