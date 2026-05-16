---
title: Durata totale pausa
description: Segnala i secondi cumulativi trascorsi dal visualizzatore in pausa durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.pauseTime` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.pauseTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
