---
title: Posizione annuncio nel pod
description: Segnala la posizione con indice zero di ogni annuncio all’interno dell’interruzione pubblicitaria principale.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 7%

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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.podPosition` quando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.podPosition`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `videoadinpod`, `post_videoadinpod` |
| Audience Manager | `c_contextdata.a.media.ad.podPosition` |

## Elementi dimensionali

Ogni elemento rappresenta il valore di posizione intero (`0`, `1`, `2`, ...) segnalato all&#39;[inizio annuncio](/help/implementation/events/ads/ad-start.md).
