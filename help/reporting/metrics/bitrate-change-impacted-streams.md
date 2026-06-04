---
title: Flussi interessati dalla modifica del bitrate
description: Conta le sessioni in cui si è verificata almeno una modifica del bitrate.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 10%

---


# Flussi interessati dalla modifica del bitrate

La metrica **Flussi interessati dalla modifica del bitrate** conta le sessioni in cui si è verificata almeno una modifica del bitrate. La metrica è un valore booleano a livello di sessione: più modifiche del bitrate all’interno dello stesso conteggio di sessioni rispetto a un flusso interessato. Per il volume totale con modifica del bitrate, utilizzare [Modifiche del bitrate](/help/reporting/dimensions/bitrate-changes.md).

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag la prima volta che viene ricevuto un evento di [modifica del bitrate](/help/implementation/events/playback/bitrate-change.md) durante la sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.bitrateChange` quando [[!UICONTROL Media Quality]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChange` |
