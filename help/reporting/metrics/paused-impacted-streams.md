---
title: Flussi interessati in pausa
description: Conta le sessioni in cui il visualizzatore si è fermato almeno una volta.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 11%

---


# Flussi interessati in pausa

La metrica **Flussi interessati dalla sospensione** conta le sessioni in cui il visualizzatore ha effettuato almeno una pausa. È un valore booleano a livello di sessione. Più pause all’interno dello stesso conteggio di sessioni come un flusso interessato. Utilizzarlo per misurare la condivisione di sessioni in cui si è verificata una pausa; per il volume totale di pausa, utilizzare [Eventi di pausa](pause-events.md).

## Come è calcolata questa metrica

Il backend multimediale imposta `mediaReporting.sessionDetails.hasPauseImpactedStreams = true` la prima volta che viene ricevuto un evento di [pausa ](/help/implementation/events/playback/pause-start.md) durante la sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.pause` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasPauseImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
