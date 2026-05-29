---
title: Numero di capitoli
description: Riporta il numero di capitoli avviati durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 9%

---


# Numero di capitoli

La metrica **Numero di capitoli** riporta il numero di capitoli avviati durante una sessione. Utilizzala per confrontare il consumo dei capitoli tra i contenuti. Per i conteggi di inizio capitolo ruotati per dimensioni capitolo (nome capitolo, posizione), utilizza la metrica Inizio capitolo disponibile quando la categoria di variabili Capitoli è abilitata.

## Come è calcolata questa metrica

Il backend multimediale incrementa questo conteggio su ogni evento [inizio capitolo](/help/implementation/events/chapters/chapter-start.md) ricevuto durante la sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Crea una [regola di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che mappa `a.media.chapterCount` a un evento personalizzato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.chapterCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (l&#39;evento personalizzato mappato dalla regola di elaborazione `a.media.chapterCount` a; vedi la ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
