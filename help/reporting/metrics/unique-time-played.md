---
title: Tempo di riproduzione univoco
description: Segnala i secondi di contenuti distinti visualizzati durante una sessione, deduplicando le ripetizioni di ricerca.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 8%

---


# Tempo di riproduzione univoco

La metrica **Tempo di riproduzione univoco** riporta i secondi di contenuti distinti visualizzati durante una sessione, deduplicando i segmenti riprodotti tramite la ricerca. Rispetto a [Tempo contenuto trascorso](content-time-spent.md), il tempo specifico riprodotto è inferiore quando un visualizzatore ricontrolla una parte dello stesso contenuto all&#39;interno della stessa sessione.

## Come è calcolata questa metrica

Il backend multimediale traccia gli intervalli della testina di riproduzione visualizzati durante la sessione e riassume la loro unione. La riproduzione dello stesso segmento di cinque secondi per due volte conta ancora cinque secondi. La metrica viene segnalata nella chiamata di chiusura. Il valore viene visualizzato come `HH:MM:SS` in Analysis Workspace e in secondi in Feed dati, Data Warehouse e API di reporting.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.uniqueTimePlayed` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.uniqueTimePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.uniqueTimePlayed` |
