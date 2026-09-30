---
title: Eventi di errore
description: Conta gli eventi di errore per somme e medie tra sessioni.
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
source-wordcount: '182'
ht-degree: 8%
---

# Eventi di errore

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica **Eventi di errore**. Adobe Analytics compila automaticamente una dimensione [Errori](/help/reporting/dimensions/errors.md) associata dalla stessa variabile di dati di contesto `a.media.qoe.errorCount`. Customer Journey Analytics espone un singolo campo `xdm.mediaReporting.qoeDataDetails.errorCount` che è possibile utilizzare come dimensione o come metrica.*

>[!ENDSHADEBOX]

La metrica **Eventi di errore** conta gli eventi di errore nelle sessioni, adatti a somme, medie e rollup percentili. Utilizza la metrica per calcolare il volume di errore totale in un periodo di rapporto e confrontare i tassi di errore tra contenuti, reti o lettori.

## Come è calcolata questa metrica

Il backend multimediale incrementa il conteggio in base a ogni errore segnalato dal lettore. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.errorCount` quando [[!UICONTROL Media Quality]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.errorCount` |

Per il reporting booleano a livello di sessione (se si è verificato un errore), utilizza [Flussi interessati dall&#39;errore](error-impacted-streams.md).
