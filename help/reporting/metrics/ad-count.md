---
title: Conteggio annunci
description: Segnala il numero di annunci avviati durante una sessione.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 9%
---

# Conteggio annunci

La metrica **Conteggio annunci** riporta il numero di annunci avviati durante una sessione. Utilizzalo per comprendere il caricamento degli annunci in base al contenuto, al canale o al tipo di flusso. Per i conteggi di inizio annuncio pivot per dimensioni annuncio (inserzionista, campagna, creativo), utilizza la metrica Avvii annuncio disponibile quando la categoria di variabili Annunci è abilitata.

## Come è calcolata questa metrica

Il backend multimediale incrementa questo conteggio su ogni evento [ad start](/help/implementation/events/ads/ad-start.md) ricevuto durante la sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che mappa `a.media.adCount` a un evento personalizzato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adCount`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (l&#39;evento personalizzato mappato dalla regola di elaborazione `a.media.adCount` a; vedi la ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
