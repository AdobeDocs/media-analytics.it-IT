---
title: Avvio file multimediale
description: Conta ogni sessione multimediale avviata, comprese le sessioni terminate con annunci pre-roll o buffering.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 7%

---


# Avvio file multimediale

La metrica **Avvii file multimediali** conta ogni sessione multimediale avviata. Viene incrementato non appena il backend riceve un evento `media.sessionStart`, anche se il visualizzatore abbandona durante gli annunci pre-roll, il buffering o prima della riproduzione di qualsiasi contenuto principale. Utilizzala come la metrica più ampia tra quelle top di funnel per i rapporti multimediali; abbinala a [Inizio contenuto](content-starts.md) per misurare la perdita di annunci e buffer.

## Come è calcolata questa metrica

Il backend multimediale imposta `mediaReporting.sessionDetails.isViewed = true` quando viene ricevuto un evento `media.sessionStart`. La metrica riportata è `1` per sessione. L’avvio del contenuto multimediale viene segnalato nella chiamata di avvio, non nella chiamata di chiusura. È l’unica metrica di Fase 1 che non attende la chiusura della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.view` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
