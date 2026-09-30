---
title: ID sito
description: Segnala l’identificatore del sito dell’annuncio per ogni annuncio.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
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
