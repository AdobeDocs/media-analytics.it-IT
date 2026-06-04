---
title: Fotogrammi persi (metrica)
description: Riporta i fotogrammi saltati cumulativi per somme e medie tra sessioni.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 7%

---


# Fotogrammi persi (metrica)

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica **Frame saltati**. Adobe Analytics compila automaticamente un [fotogramma (dimensione)](/help/reporting/dimensions/dropped-frames.md) accoppiato dalla stessa variabile di dati di contesto `a.media.qoe.droppedFrameCount`. Customer Journey Analytics espone un singolo campo `xdm.mediaReporting.qoeDataDetails.droppedFrames` che è possibile utilizzare come dimensione o come metrica. Per informazioni su come raccogliere questa variabile, vedere [Frame rilasciati](/help/implementation/variables/quality/dropped-frames.md).*

>[!ENDSHADEBOX]

La metrica **Fotogrammi rilasciati** riporta i fotogrammi rilasciati cumulativi tra sessioni, adatti a somme, medie e aggregazioni percentili. Utilizza la metrica per calcolare il calo totale del volume in un periodo di reporting e confrontare la qualità del rendering dei frame tra contenuti, reti o lettori.

## Come è calcolata questa metrica

Il lettore aggiorna il valore `droppedFrames` dell&#39;oggetto QoE mentre si accumulano le gocce. Il backend riporta il valore più recente nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.droppedFrameCount` quando [[!UICONTROL Media Quality]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

Per il reporting booleano a livello di sessione (se sono stati eliminati dei fotogrammi), utilizza [Flussi interessati da fotogrammi saltati](dropped-frame-impacted-streams.md).
