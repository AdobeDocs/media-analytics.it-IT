---
title: ID sito
description: Segnala l’identificatore del sito dell’annuncio per ogni annuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 10%

---


# ID sito

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **ID sito**. Per informazioni su come raccogliere questa variabile, vedere [ID sito](/help/implementation/variables/ads/site-id.md).*

>[!ENDSHADEBOX]

La dimensione **ID sito** riporta l&#39;identificatore del sito dell&#39;annuncio (in genere un ID dalla piattaforma dell&#39;ad-server). Utilizza la dimensione per suddividere il coinvolgimento in base al sito di posizionamento degli annunci.

## Compilazione di questa dimensione

L&#39;ID sito viene impostato dal lettore a ogni evento [ad start](/help/implementation/events/ads/ad-start.md).

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Crea una [regola di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.ad.site` a un eVar. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.siteID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l&#39;eVar a cui la regola di elaborazione mappa `a.media.ad.site`) |
| Audience Manager | `c_contextdata.a.media.ad.site` |

## Elementi dimensionali

Ogni elemento rappresenta il valore letterale dell&#39;ID sito segnalato all&#39;[inizio annuncio](/help/implementation/events/ads/ad-start.md).
