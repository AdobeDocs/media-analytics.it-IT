---
title: Eventi di errore
description: Conta gli eventi di errore per somme e medie tra sessioni.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 7%

---


# Eventi di errore

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica **Eventi di errore**. Adobe Analytics compila automaticamente una dimensione [Errori](/help/reporting/dimensions/errors.md) associata dalla stessa variabile di dati di contesto `a.media.qoe.errorCount`. Customer Journey Analytics espone un singolo campo `mediaReporting.qoeDataDetails.errorCount` che è possibile utilizzare come dimensione o come metrica.*

>[!ENDSHADEBOX]

La metrica **Eventi di errore** conta gli eventi di errore nelle sessioni, adatti a somme, medie e rollup percentili. Utilizza la metrica per calcolare il volume di errore totale in un periodo di rapporto e confrontare i tassi di errore tra contenuti, reti o lettori.

## Come è calcolata questa metrica

Il backend multimediale incrementa il conteggio in base a ogni errore segnalato dal lettore. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.errorCount` quando [[!UICONTROL Media Quality]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |

Per il reporting booleano a livello di sessione (se si è verificato un errore), utilizza [Flussi interessati dall&#39;errore](error-impacted-streams.md).
