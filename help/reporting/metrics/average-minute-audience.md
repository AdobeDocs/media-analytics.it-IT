---
title: Pubblico medio per minuto
description: Riporta il numero medio di visualizzatori che guardano in un dato minuto nel runtime del contenuto.
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
source-wordcount: '171'
ht-degree: 12%
---

# Pubblico medio per minuto

La metrica **Pubblico medio per minuto** riporta il numero medio di visualizzatori che guardano in un dato minuto nel runtime del contenuto. È la misura &quot;AMA&quot; standard utilizzata per confrontare la portata dei contenuti multimediali tra contenuti di diverse lunghezze.

## Come è calcolata questa metrica

Il backend multimediale calcola il pubblico medio per minuto per sessione come `Content time spent / Content length`. Quando riepilogato nelle sessioni, il totale rappresenta la dimensione media del pubblico a ogni minuto del contenuto. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.averageMinuteAudience` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.averageMinuteAudience`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.averageMinuteAudience` |

>[!IMPORTANT]
>
>Il pubblico medio per minuto richiede una [lunghezza contenuto](/help/reporting/dimensions/content-length.md) diversa da zero. Se la lunghezza del contenuto non è impostata o è zero, questa metrica non viene prodotta per la sessione.
