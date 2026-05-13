---
title: Flussi interessati dalla modifica del bitrate
description: Conta le sessioni in cui si è verificata almeno una modifica del bitrate.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 9%

---


# Flussi interessati dalla modifica del bitrate

La metrica **Flussi interessati dalla modifica del bitrate** conta le sessioni in cui si è verificata almeno una modifica del bitrate. La metrica è un valore booleano a livello di sessione: più modifiche del bitrate all’interno dello stesso conteggio di sessioni rispetto a un flusso interessato. Per il volume totale con modifica del bitrate, utilizzare [Modifiche del bitrate](/help/reporting/dimensions/bitrate-changes.md).

## Come è calcolata questa metrica

Il backend multimediale imposta `mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams = true` la prima volta che un evento `media.bitrateChange` viene ricevuto durante la sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.bitrateChange` quando [[!UICONTROL Media Quality]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
