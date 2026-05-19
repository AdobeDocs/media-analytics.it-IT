---
title: Avvio file multimediale
description: Conta ogni sessione multimediale avviata, comprese le sessioni terminate con annunci pre-roll o buffering.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 6%

---


# Avvio file multimediale

La metrica **Avvii file multimediali** conta ogni sessione multimediale avviata. Viene incrementato non appena il backend riceve un evento [inizio sessione](/help/implementation/events/session/session-start.md), anche se il visualizzatore si abbandona durante gli annunci pre-roll, il buffering o prima della riproduzione di qualsiasi contenuto principale. Utilizzala come la metrica più ampia tra quelle top di funnel per i rapporti multimediali; abbinala a [Inizio contenuto](content-starts.md) per misurare la perdita di annunci e buffer.

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag quando viene ricevuto un evento di [inizio sessione](/help/implementation/events/session/session-start.md). La metrica riportata è `1` per sessione. L’avvio del file multimediale viene segnalato nella chiamata di avvio, non nella chiamata di chiusura; è l’unica metrica che non attende la chiusura della sessione. Tutte le altre metriche multimediali, tra cui [Inizio contenuto](/help/reporting/metrics/content-starts.md), [Tempo contenuto trascorso](/help/reporting/metrics/content-time-spent.md) e [Indicatori avanzamento](/help/reporting/metrics/progress-markers.md), vengono segnalate nella chiamata di chiusura e non sono disponibili in tempo reale durante la riproduzione. [Inizio annuncio](/help/reporting/metrics/ad-starts.md) è l&#39;unica metrica aggiuntiva riportata sull&#39;evento di attivazione anziché alla chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.view` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.view` |
