---
title: Flussi interessati da errori
description: Conta le sessioni in cui si è verificato almeno un errore.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 10%

---


# Flussi interessati da errori

La metrica **Flussi interessati dall&#39;errore** conta le sessioni in cui si è verificato almeno un errore (`trackError` è stato chiamato o un evento [error](/help/implementation/events/error.md) generato). La metrica è un valore booleano a livello di sessione: più errori all’interno dello stesso conteggio di sessioni come un flusso interessato. Per il volume totale degli errori, utilizzare [Errori](/help/reporting/dimensions/errors.md).

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag la prima volta che viene ricevuto un evento [error](/help/implementation/events/error.md) durante la sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.error` quando [[!UICONTROL Media Quality]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasErrorImpactedStreams`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.error` |
