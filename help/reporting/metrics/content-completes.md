---
title: Completamenti contenuto
description: Conta le sessioni la cui testina di riproduzione ha raggiunto la fine del contenuto.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 10%

---


# Completamenti contenuto

La metrica **Completamenti del contenuto** conta le sessioni la cui testina di riproduzione ha raggiunto la fine del contenuto. Associalo a [Il contenuto inizia](content-starts.md) per calcolare il tasso di completamento; associalo a [Inizi file multimediali](media-starts.md) per calcolare il tasso di visualizzazione end-to-end.

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag quando viene ricevuto un evento [sessione completata](/help/implementation/events/session/session-complete.md). La metrica viene segnalata nella chiamata di chiusura. Una sessione in timeout senza un `sessionComplete` esplicito non viene conteggiata come completamento.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.complete` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isCompleted`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.complete` |
