---
title: Conteggio annunci
description: Segnala il numero di annunci avviati durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%

---


# Conteggio annunci

La metrica **Conteggio annunci** riporta il numero di annunci avviati durante una sessione. Utilizzalo per comprendere il caricamento degli annunci in base al contenuto, al canale o al tipo di flusso. Per i conteggi di inizio annuncio pivot per dimensioni annuncio (inserzionista, campagna, creativo), utilizza la metrica Avvii annuncio disponibile quando la categoria di variabili Annunci è abilitata.

## Come è calcolata questa metrica

Il backend multimediale incrementa `mediaReporting.sessionDetails.adCount` su ogni evento `media.adStart` ricevuto durante la sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che mappa `a.media.adCount` a un evento personalizzato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.adCount`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (l&#39;evento personalizzato mappato dalla regola di elaborazione `a.media.adCount` a; vedi la ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
