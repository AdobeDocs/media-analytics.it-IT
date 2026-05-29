---
title: Perdite prima dell’inizio
description: Conta le sessioni in cui il visualizzatore si chiude prima di eseguire il rendering di qualsiasi contenuto principale.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 7%

---


# Perdite prima dell’inizio

La metrica **Perde prima dell&#39;inizio** conta le sessioni in cui il visualizzatore si chiude prima di eseguire il rendering di qualsiasi contenuto principale. La metrica contrassegna l’abbandono pre-contenuto indipendentemente dal comportamento dell’annuncio, quindi è la migliore misura del drop-off puro pre-contenuto. Associalo a [Avvii file multimediali](/help/reporting/metrics/media-starts.md) e [Inizio contenuto](/help/reporting/metrics/content-starts.md) per calcolare la condivisione di sessioni che non hanno mai prodotto un frame di contenuto.

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag per le sessioni che si chiudono senza mai produrre un evento [play](/help/implementation/events/playback/play.md) sul contenuto principale. La metrica viene segnalata nella chiamata di chiusura. Gli scenari comuni includono: il visualizzatore esce durante un annuncio pre-roll, il lettore si ferma indefinitamente nella fase iniziale del buffer, o un errore si attiva prima del primo evento di riproduzione del contenuto principale. In tutti questi casi la sessione registra un [Avvio file multimediale](/help/reporting/metrics/media-starts.md) ma non un [Avvio contenuto](/help/reporting/metrics/content-starts.md) e non vengono registrati [Indicatori di avanzamento](/help/reporting/metrics/progress-markers.md).

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.dropBeforeStart` quando [[!UICONTROL Media Quality]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.isDroppedBeforeStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.dropBeforeStart` |
