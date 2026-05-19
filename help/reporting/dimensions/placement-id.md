---
title: ID posizionamento
description: Segnala l’identificatore di posizionamento di ciascun annuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 10%

---


# ID posizionamento

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **ID posizionamento**. Per informazioni su come raccogliere questa variabile, vedere [ID posizionamento](/help/implementation/variables/ads/placement-id.md).*

>[!ENDSHADEBOX]

La dimensione **ID posizionamento** riporta l&#39;identificatore di posizionamento dell&#39;annuncio (in genere uno slot o una zona definita nella piattaforma ad-server). Utilizza la dimensione per confrontare il coinvolgimento e il completamento tra gli slot di posizionamento.

## Compilazione di questa dimensione

L&#39;ID posizionamento viene impostato dal lettore a ogni evento [ad start](/help/implementation/events/ads/ad-start.md).

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.ad.placement` a un eVar. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.placementID`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l&#39;eVar a cui la regola di elaborazione mappa `a.media.ad.placement`) |
| Audience Manager | `c_contextdata.a.media.ad.placement` |

## Elementi dimensionali

Ogni elemento rappresenta il valore di posizionamento letterale riportato all&#39;[inizio annuncio](/help/implementation/events/ads/ad-start.md).
