---
title: Eventi di pausa
description: Conta ogni pausa distinta che si è verificata durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 10%

---


# Eventi di pausa

La metrica **Eventi di pausa** conta ogni evento `media.pauseStart` distinto ricevuto durante una sessione, incluse più pause all&#39;interno della stessa sessione. Associalo a [Durata totale pausa](total-pause-duration.md) per derivare la lunghezza media della pausa e a [Flussi interessati in pausa](paused-impacted-streams.md) per contare le sessioni in pausa almeno una volta.

## Come è calcolata questa metrica

Il backend multimediale incrementa `mediaReporting.sessionDetails.pauseCount` a ogni evento `media.pauseStart`. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.pauseCount` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.pauseCount`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
