---
title: Completamenti contenuto
description: Conta le sessioni la cui testina di riproduzione ha raggiunto la fine del contenuto.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 10%

---


# Completamenti contenuto

La metrica **Completamenti del contenuto** conta le sessioni la cui testina di riproduzione ha raggiunto la fine del contenuto. Associalo a [Il contenuto inizia](content-starts.md) per calcolare il tasso di completamento; associalo a [Inizi file multimediali](media-starts.md) per calcolare il tasso di visualizzazione end-to-end.

## Come è calcolata questa metrica

Il backend multimediale imposta `mediaReporting.sessionDetails.isCompleted = true` quando viene ricevuto un evento [sessione completata](/help/implementation/events/session/session-complete.md). La metrica viene segnalata nella chiamata di chiusura. Una sessione in timeout senza un `sessionComplete` esplicito non viene conteggiata come completamento.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.complete` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isCompleted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.complete` |
