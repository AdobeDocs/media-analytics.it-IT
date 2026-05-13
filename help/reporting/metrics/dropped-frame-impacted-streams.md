---
title: Flussi interessati da fotogrammi saltati
description: Conta le sessioni in cui è stato eliminato almeno un frame.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 10%

---


# Flussi interessati da fotogrammi saltati

La metrica **Flussi interessati da fotogrammi saltati** conta le sessioni in cui è stato eliminato almeno un fotogramma. La metrica è un valore booleano a livello di sessione: più cadute all’interno dello stesso conteggio di sessioni di un flusso interessato. Per il volume di rilascio totale, utilizzare [Frame rilasciati](dropped-frames.md).

## Come è calcolata questa metrica

Il backend multimediale imposta `mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams = true` se il valore `droppedFrames` dell&#39;oggetto QoE è maggiore di zero alla chiusura della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.droppedFrames` quando [[!UICONTROL Media Quality]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
