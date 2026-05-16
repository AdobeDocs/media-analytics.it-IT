---
title: Tempo trascorso su capitolo
description: Segnala i secondi totali di riproduzione attiva per capitolo.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 9%

---


# Tempo trascorso su capitolo

La metrica **Durata capitolo** riporta il totale dei secondi di riproduzione attiva per capitolo. Associalo a [Durata capitolo](/help/reporting/dimensions/chapter-length.md) per calcolare la quota di ciascun capitolo utilizzato.

## Come è calcolata questa metrica

Il backend multimediale somma il tempo wall-clock trascorso tra gli eventi mentre il lettore si trova nello stato `play` su un capitolo. Sono esclusi i tempi di pausa, buffering e blocchi. La metrica viene segnalata nella chiamata di chiusura del capitolo. Il valore viene visualizzato come `HH:MM:SS` in Analysis Workspace e in secondi in Feed dati, Data Warehouse e API di reporting.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.chapter.timePlayed` quando [[!UICONTROL Media Chapters]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.timePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.chapter.timePlayed` |
