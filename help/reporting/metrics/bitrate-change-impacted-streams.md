---
title: Flussi interessati dalla modifica del bitrate
description: Conta le sessioni in cui si è verificata almeno una modifica del bitrate.
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
source-wordcount: '143'
ht-degree: 10%
---

# Flussi interessati dalla modifica del bitrate

La metrica **Flussi interessati dalla modifica del bitrate** conta le sessioni in cui si è verificata almeno una modifica del bitrate. La metrica è un valore booleano a livello di sessione; più modifiche del bitrate all’interno dello stesso conteggio di sessioni di un flusso interessato. Per il volume totale con modifica del bitrate, utilizzare [Modifiche del bitrate](/help/reporting/dimensions/bitrate-changes.md).

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag la prima volta che viene ricevuto un evento di [modifica del bitrate](/help/implementation/events/playback/bitrate-change.md) durante la sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.bitrateChange` quando [[!UICONTROL Media Quality]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChange` |
