---
title: Flussi interessati in pausa
description: Conta le sessioni in cui il visualizzatore si è fermato almeno una volta.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 11%

---


# Flussi interessati in pausa

La metrica **Flussi interessati dalla sospensione** conta le sessioni in cui il visualizzatore ha effettuato almeno una pausa. È un valore booleano a livello di sessione. Più pause all’interno dello stesso conteggio di sessioni come un flusso interessato. Utilizzarlo per misurare la condivisione di sessioni in cui si è verificata una pausa; per il volume totale di pausa, utilizzare [Eventi di pausa](pause-events.md).

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag la prima volta che viene ricevuto un evento di [pausa &#x200B;](/help/implementation/events/playback/pause-start.md) durante la sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.pause` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasPauseImpactedStreams`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
