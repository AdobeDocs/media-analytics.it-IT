---
title: Eventi di arresto
description: Conta gli eventi di stallo per somme e medie tra sessioni.
feature: Metrics
role: User, Admin
source-git-commit: 1278355e0bfc67c635250c426edaf865fb658c37
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 7%

---


# Eventi di arresto

La metrica **Eventi di stallo** conta gli eventi di stallo tra sessioni, adatti a somme, medie e aggregazioni percentili. Utilizza la metrica per calcolare il volume totale di stall in un periodo di report e confrontare la stabilità di stall tra contenuti, reti o lettori.

In Customer Journey Analytics, `mediaReporting.qoeDataDetails.stallCount` può essere utilizzato come metrica o come dimensione senza un componente dimensione separato.

## Come è calcolata questa metrica

Il back-end multimediale incrementa il conteggio ogni volta che non viene registrato alcun movimento della testina di riproduzione sul contenuto principale per almeno tre eventi consecutivi. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Crea una [regola di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che mappa `a.media.qoe.stallCount` a un evento personalizzato. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.stallCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (l&#39;evento personalizzato mappato dalla regola di elaborazione `a.media.qoe.stallCount` a; vedi la ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stallCount` |

Per il reporting booleano a livello di sessione (se si è verificato un arresto), utilizza [Flussi interessati da un arresto](stall-impacted-streams.md).
