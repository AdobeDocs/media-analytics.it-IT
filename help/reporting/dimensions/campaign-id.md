---
title: ID campagna
description: Segnala la campagna a cui appartiene ogni annuncio.
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
source-wordcount: '120'
ht-degree: 15%
---

# ID campagna

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **ID campagna**. Per informazioni su come raccogliere questa variabile, consulta [ID campagna](/help/implementation/variables/ads/campaign-id.md).*

>[!ENDSHADEBOX]

La dimensione **ID campagna** riporta la campagna pubblicitaria a cui appartiene ogni contenuto creativo dell&#39;annuncio. Utilizza la dimensione per aggregare il coinvolgimento tra più creativi che condividono una campagna.

## Compilazione di questa dimensione

L&#39;ID della campagna è impostato dal lettore a ogni evento [ad start](/help/implementation/events/ads/ad-start.md).

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.campaign` quando [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `videocampaign`, `post_videocampaign` |
| Audience Manager | `c_contextdata.a.media.ad.campaign` |

## Elementi dimensionali

Ogni elemento è il valore letterale della campagna riportato al [inizio annuncio](/help/implementation/events/ads/ad-start.md).
