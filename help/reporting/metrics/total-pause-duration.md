---
title: Durata totale pausa
description: Segnala i secondi cumulativi trascorsi dal visualizzatore in pausa durante una sessione.
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
source-wordcount: '162'
ht-degree: 10%
---

# Durata totale pausa

La metrica **Durata totale pausa** riporta i secondi cumulativi trascorsi dal visualizzatore in pausa durante una sessione. La metrica è la somma di tutti gli intervalli tra ogni evento [pause start](/help/implementation/events/playback/pause-start.md) e il successivo evento [play](/help/implementation/events/playback/play.md). Più pause vengono aggiunte insieme. Associa [Eventi di pausa](pause-events.md) per derivare la lunghezza media della pausa.

## Come è calcolata questa metrica

Il backend multimediale somma il tempo di clock a parete trascorso tra ogni evento [inizio pausa](/help/implementation/events/playback/pause-start.md) e l&#39;evento [riproduzione](/help/implementation/events/playback/play.md) corrispondente. La metrica viene segnalata nella chiamata di chiusura. Il valore viene visualizzato come `HH:MM:SS` in Analysis Workspace e in secondi altrove.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.pauseTime` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.pauseTime`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
