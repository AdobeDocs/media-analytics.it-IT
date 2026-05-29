---
title: Pubblico medio per minuto
description: Riporta il numero medio di visualizzatori che guardano in un dato minuto nel runtime del contenuto.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.averageMinuteAudience` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.averageMinuteAudience`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.averageMinuteAudience` |

>[!IMPORTANT]
>
>Il pubblico medio per minuto richiede una [lunghezza contenuto](/help/reporting/dimensions/content-length.md) diversa da zero. Se la lunghezza del contenuto non è impostata o è zero, questa metrica non viene prodotta per la sessione.
