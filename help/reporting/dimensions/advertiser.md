---
title: Inserzionista
description: Segnala l’azienda o il brand presente in ogni annuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 12%

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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.advertiser` quando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `videoadvertiser`, `post_videoadvertiser` |
| Audience Manager | `c_contextdata.a.media.ad.advertiser` |

## Elementi dimensionali

Ogni elemento è il nome letterale dell&#39;inserzionista riportato all&#39;[inizio annuncio](/help/implementation/events/ads/ad-start.md).
