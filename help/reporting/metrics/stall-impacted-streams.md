---
title: Flussi interessati da interruzioni
description: Conta le sessioni in cui si è verificato almeno un arresto durante la riproduzione.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 8%

---


# Flussi interessati da interruzioni

La metrica **Flussi interessati dallo stallo** conta le sessioni in cui si è verificato almeno un arresto durante la riproduzione. La metrica è un valore booleano a livello di sessione: più blocchi all’interno dello stesso conteggio di sessioni come un flusso interessato. Per il volume totale di stall, utilizzare [Eventi di stall](stall-events.md).

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag quando non viene registrato alcun movimento dell’indicatore di riproduzione sul contenuto principale per almeno tre eventi consecutivi durante la sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Crea una [regola di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che mappa `a.media.qoe.stall` a un evento personalizzato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasStallImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (l&#39;evento personalizzato mappato dalla regola di elaborazione `a.media.qoe.stall` a; vedi la ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stall` |
