---
title: Flussi interessati dal buffer
description: Conta le sessioni in cui il lettore è entrato in uno stato buffer almeno una volta.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 9%

---


# Flussi interessati dal buffer

La metrica **Flussi interessati dal buffer** conta le sessioni in cui il lettore è entrato almeno una volta in uno stato buffer. La metrica è un valore booleano a livello di sessione: più eventi buffer all’interno dello stesso conteggio di sessione come un flusso interessato. Per il volume totale del buffer, utilizzare [Eventi buffer](buffer-events.md).

## Come è calcolata questa metrica

Il backend multimediale imposta `mediaReporting.qoeDataDetails.hasBufferImpactedStreams = true` la prima volta che un evento `media.bufferStart` viene ricevuto durante la sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.buffer` quando [[!UICONTROL Media Quality]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasBufferImpactedStreams`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
