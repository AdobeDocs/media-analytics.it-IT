---
title: Completamenti contenuto
description: Conta le sessioni la cui testina di riproduzione ha raggiunto la fine del contenuto.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 9%

---


# Completamenti contenuto

La metrica **Completamenti del contenuto** conta le sessioni la cui testina di riproduzione ha raggiunto la fine del contenuto. Associalo a [Il contenuto inizia](content-starts.md) per calcolare il tasso di completamento; associalo a [Inizi file multimediali](media-starts.md) per calcolare il tasso di visualizzazione end-to-end.

## Come è calcolata questa metrica

Il backend multimediale imposta `mediaReporting.sessionDetails.isCompleted = true` quando viene ricevuto un evento `media.sessionComplete`. La metrica viene segnalata nella chiamata di chiusura. Una sessione in timeout senza un `sessionComplete` esplicito non viene conteggiata come completamento.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.complete` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isCompleted`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
