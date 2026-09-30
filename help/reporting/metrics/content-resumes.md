---
title: Riprende il contenuto
description: Conta le sessioni che hanno ripreso una riproduzione precedentemente interrotta.
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
source-wordcount: '169'
ht-degree: 10%
---

# Riprende il contenuto

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica di reporting **Il contenuto riprende**. Per informazioni su come raccogliere questa variabile, vedere [Riprese del contenuto](/help/implementation/variables/core/content-resumes.md).*

>[!ENDSHADEBOX]

La metrica **Il contenuto riprende** conta le sessioni che hanno ripreso una riproduzione interrotta in precedenza. Viene incrementato quando il lettore contrassegna una sessione come ripresa il `sessionStart` (ad esempio, dopo che un buffer, una pausa o un arresto hanno superato i 30 minuti). Utilizzala per separare le nuove sessioni autentiche dalle sessioni di continuazione per lo stesso visualizzatore e la stessa risorsa.

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag quando `xdm.mediaCollection.sessionDetails.hasResume` è `true` nell&#39;evento [inizio sessione](/help/implementation/events/session/session-start.md). Il lettore deve contrassegnare esplicitamente la sessione come ripresa. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.resume` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
