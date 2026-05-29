---
title: Durata totale dello stallo
description: Riporta il tempo di interruzione cumulativo per somme e medie tra sessioni.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 7%

---


# Durata totale dello stallo

La metrica **Durata totale dello stallo** riporta il tempo di stallo cumulativo tra le sessioni, adatto a somme, medie e aggregazioni percentili. Utilizza la metrica per calcolare il tempo totale impiegato dai visualizzatori per attendere la riproduzione interrotta in un periodo di reporting.

In Customer Journey Analytics, `xdm.mediaReporting.qoeDataDetails.stallTime` può essere utilizzato come metrica o come dimensione senza un componente dimensione separato.

## Come è calcolata questa metrica

Il back-end multimediale somma la durata di ogni intervallo di stallo, rilevato quando non viene registrato alcun movimento della testina di riproduzione sul contenuto principale per almeno tre eventi consecutivi. La metrica viene segnalata nella chiamata di chiusura. Analysis Workspace mostra il valore come `HH:MM:SS`; Feed dati, Data Warehouse e API di reporting mostrano il valore in secondi.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che mappa `a.media.qoe.stallTime` a un evento personalizzato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.stallTime`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (l&#39;evento personalizzato mappato dalla regola di elaborazione `a.media.qoe.stallTime` a; vedi la ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stallTime` |
