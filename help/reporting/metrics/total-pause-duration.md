---
title: Durata totale pausa
description: Segnala i secondi cumulativi trascorsi dal visualizzatore in pausa durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 8%

---


# Durata totale pausa

La metrica **Durata totale pausa** riporta i secondi cumulativi trascorsi dal visualizzatore in pausa durante una sessione. La metrica è la somma di tutti gli intervalli tra ogni `media.pauseStart` e il successivo `media.play`. Più pause vengono aggiunte insieme. Associa [Eventi di pausa](pause-events.md) per derivare la lunghezza media della pausa.

## Come è calcolata questa metrica

Il backend dei contenuti multimediali somma il tempo di wall-clock trascorso tra ogni `media.pauseStart` e l&#39;evento `media.play` corrispondente. La metrica viene segnalata nella chiamata di chiusura. Il valore viene visualizzato come `HH:MM:SS` in Analysis Workspace e in secondi altrove.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.pauseTime` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.pauseTime`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
