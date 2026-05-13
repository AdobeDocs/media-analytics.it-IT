---
title: Eventi buffer (metrica)
description: Conta gli eventi di buffering per somme e medie tra sessioni.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 7%

---


# Eventi buffer (metrica)

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica **Eventi buffer**. Adobe Analytics compila automaticamente [eventi buffer (dimensione)](/help/reporting/dimensions/buffer-events.md) associati dalla stessa variabile di dati di contesto `a.media.qoe.bufferCount`. Customer Journey Analytics espone un singolo campo `mediaReporting.qoeDataDetails.bufferCount` che è possibile utilizzare come dimensione o come metrica.*

>[!ENDSHADEBOX]

La metrica **Eventi buffer** conta gli eventi di buffering tra le sessioni, in base a somme, medie e rollup percentili. Utilizza la metrica per calcolare il volume totale del buffer in un periodo di report e per confrontare la stabilità del buffer tra contenuti, reti o lettori.

## Come è calcolata questa metrica

Il backend multimediale incrementa il conteggio ogni volta che il lettore entra in uno stato `buffer`. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.bufferCount` quando [[!UICONTROL Media Quality]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |

Per il reporting booleano a livello di sessione (se la sessione ha riscontrato un buffering), utilizza [Flussi interessati dal buffer](buffer-impacted-streams.md).
