---
title: Flussi interessati dal buffer
description: Conta le sessioni in cui il lettore è entrato in uno stato buffer almeno una volta.
feature: Metrics
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 10%

---


# Flussi interessati dal buffer

La metrica **Flussi interessati dal buffer** conta le sessioni in cui il lettore è entrato almeno una volta in uno stato buffer. La metrica è un valore booleano a livello di sessione; più eventi buffer all’interno dello stesso numero di sessioni corrispondono a un flusso interessato. Per il volume totale del buffer, utilizzare [Eventi buffer](buffer-events.md).

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag la prima volta che viene ricevuto un evento [buffer start](/help/implementation/events/playback/buffer-start.md) durante la sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.buffer` quando [[!UICONTROL Media Quality]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasBufferImpactedStreams`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.buffer` |
