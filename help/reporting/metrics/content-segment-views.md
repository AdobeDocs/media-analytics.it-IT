---
title: Visualizzazioni del segmento di contenuto
description: Conta i segmenti in cui si è verificata la riproduzione attiva del contenuto principale.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 9%

---


# Visualizzazioni del segmento di contenuto

La metrica **Visualizzazioni del segmento di contenuto** conta segmenti di contenuto di cinque minuti in cui si è verificata la riproduzione attiva del contenuto principale. La metrica conferma che il visualizzatore ha riprodotto il contenuto in quel segmento invece di caricare o buffering. Associalo alla dimensione [Segmento di contenuto](/help/reporting/dimensions/content-segment.md) per suddividere quali porzioni di visualizzatori di contenuti a lunga forma sono state effettivamente utilizzate.

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag per qualsiasi chiamata di chiusura che copre un segmento in cui è stato ricevuto almeno un evento [play](/help/implementation/events/playback/play.md) per il contenuto principale. La metrica viene segnalata nella chiamata di chiusura. Nel percorso API di Media Edge, le visualizzazioni dei segmenti vengono attivate nella stessa condizione in cui inizia il contenuto. Entrambi richiedono un evento [play](/help/implementation/events/playback/play.md) sul contenuto principale.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.segmentView` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasSegmentView`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
