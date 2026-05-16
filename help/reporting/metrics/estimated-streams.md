---
title: Flussi stimati
description: Approssimazione del numero di flussi audio o video per sessione.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 10%

---


# Flussi stimati

La metrica **Flussi stimati** si avvicina al numero di flussi audio o video per sessione, con un flusso conteggiato per ogni 30 minuti di riproduzione totale. È destinato agli accordi di sindacazione dei contenuti e a raggiungere approssimazioni in cui ogni blocco di consumo di 30 minuti conta come un &quot;flusso&quot; separato.

## Come è calcolata questa metrica

Il backend multimediale calcola `mediaReporting.sessionDetails.estimatedStreams = FLOOR(totalTimePlayed / 1800) + 1`, dove `totalTimePlayed` è [Tempo trascorso](media-time-spent.md) in secondi. La metrica viene segnalata nella chiamata di chiusura.

| Tempo trascorso dei contenuti multimediali | Flussi stimati |
| --- | --- |
| 0-29 min. | 1 |
| 30-59 min. | 2 |
| 60-89 min. | 3 |
| 90+ min | 4+ |

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che mappa `a.media.estimatedStreams` a un evento personalizzato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.estimatedStreams`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (l&#39;evento personalizzato mappato dalla regola di elaborazione `a.media.estimatedStreams` a; vedi la ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.estimatedStreams` |
