---
title: Inserzionista
description: Segnala l’azienda o il brand presente in ogni annuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 11%

---


# Inserzionista

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Inserzionista**. Per informazioni su come raccogliere questa variabile, consulta [Inserzionista](/help/implementation/variables/ads/advertiser.md).*

>[!ENDSHADEBOX]

La dimensione **Inserzionista** riporta l&#39;azienda o il brand presente in ogni annuncio (ad esempio, `"Ford"` o `"Coca-Cola"`). Utilizza la dimensione per interrompere il coinvolgimento e il completamento da parte dell’inserzionista.

## Compilazione di questa dimensione

L&#39;inserzionista è impostato dal lettore a ogni evento `media.adStart`.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.advertiser` quando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `videoadvertiser, post_videoadvertiser` |

## Elementi dimensionali

Ogni elemento è il nome letterale dell&#39;inserzionista riportato in `media.adStart`.
