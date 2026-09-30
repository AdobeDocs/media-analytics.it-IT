---
title: Durata totale dello stallo
description: Riporta il tempo di interruzione cumulativo per somme e medie tra sessioni.
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
| Adobe Analytics | Crea una [regola di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che mappa `a.media.qoe.stallTime` a un evento personalizzato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.stallTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (l&#39;evento personalizzato mappato dalla regola di elaborazione `a.media.qoe.stallTime` a; vedi la ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stallTime` |
