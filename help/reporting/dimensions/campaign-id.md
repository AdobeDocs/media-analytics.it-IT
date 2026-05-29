---
title: ID campagna
description: Segnala la campagna a cui appartiene ogni annuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 13%

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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.campaign` quando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `videocampaign`, `post_videocampaign` |
| Audience Manager | `c_contextdata.a.media.ad.campaign` |

## Elementi dimensionali

Ogni elemento è il valore letterale della campagna riportato al [inizio annuncio](/help/implementation/events/ads/ad-start.md).
