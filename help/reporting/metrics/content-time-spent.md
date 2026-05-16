---
title: Tempo trascorso dei contenuti
description: Segnala i secondi totali di riproduzione dei contenuti principali attivi per sessione.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 8%

---


# Tempo trascorso dei contenuti

La metrica **Tempo contenuto trascorso** riporta i secondi totali di riproduzione del contenuto principale attivo per sessione, esclusi annunci, pause, buffering e blocchi. Utilizzala come metrica di coinvolgimento per la visualizzazione dei contenuti; per il tempo trascorso, inclusi gli annunci, consulta [Tempo trascorso sui contenuti multimediali](media-time-spent.md).

## Come è calcolata questa metrica

Il backend multimediale somma il tempo wall-clock trascorso tra gli eventi mentre il lettore è nello stato `play` sul contenuto principale. È escluso il tempo durante annunci, pause, eventi buffer e blocchi. La metrica viene segnalata nella chiamata di chiusura. Il valore viene visualizzato come `HH:MM:SS` in Analysis Workspace e in secondi in Feed dati, Data Warehouse e API di reporting.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.timePlayed` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.timePlayed`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.timePlayed` |
