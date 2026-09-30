---
title: Inserzionista
description: Segnala l’azienda o il brand presente in ogni annuncio.
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
source-wordcount: '115'
ht-degree: 13%
---

# Inserzionista

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Inserzionista**. Per informazioni su come raccogliere questa variabile, consulta [Inserzionista](/help/implementation/variables/ads/advertiser.md).*

>[!ENDSHADEBOX]

La dimensione **Inserzionista** riporta l&#39;azienda o il brand presente in ogni annuncio (ad esempio, `"Ford"` o `"Coca-Cola"`). Utilizza la dimensione per interrompere il coinvolgimento e il completamento da parte dell’inserzionista.

## Compilazione di questa dimensione

L&#39;inserzionista è impostato dal lettore a ogni evento [inizio annuncio](/help/implementation/events/ads/ad-start.md).

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.advertiser` quando [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `videoadvertiser`, `post_videoadvertiser` |
| Audience Manager | `c_contextdata.a.media.ad.advertiser` |

## Elementi dimensionali

Ogni elemento è il nome letterale dell&#39;inserzionista riportato all&#39;[inizio annuncio](/help/implementation/events/ads/ad-start.md).
