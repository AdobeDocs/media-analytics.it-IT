---
title: Posizione annuncio nel pod
description: Segnala la posizione con indice zero di ogni annuncio all’interno dell’interruzione pubblicitaria principale.
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
source-wordcount: '154'
ht-degree: 9%
---

# Posizione annuncio nel pod

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la dimensione di reporting **Annuncio in posizione pod**. Per informazioni su come raccogliere questa variabile, vedere [Annuncio nella posizione pod](/help/implementation/variables/ads/ad-in-pod-position.md).*

>[!ENDSHADEBOX]

La dimensione **Annuncio in posizione pod** riporta la posizione con indice zero di ciascun annuncio all&#39;interno dell&#39;interruzione pubblicitaria padre. Il primo annuncio in un pod è `0`, il secondo è `1` e così via. Utilizza la dimensione per confrontare il coinvolgimento e il completamento in base alla posizione all’interno di un’interruzione pubblicitaria.

## Compilazione di questa dimensione

La posizione dell&#39;annuncio nel pod viene impostata dal lettore a ogni evento [inizio annuncio](/help/implementation/events/ads/ad-start.md).

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.podPosition` quando [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.podPosition`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `videoadinpod`, `post_videoadinpod` |
| Audience Manager | `c_contextdata.a.media.ad.podPosition` |

## Elementi dimensionali

Ogni elemento rappresenta il valore di posizione intero (`0`, `1`, `2`, ...) segnalato all&#39;[inizio annuncio](/help/implementation/events/ads/ad-start.md).
