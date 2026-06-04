---
title: Nome annuncio
description: Riporta il titolo leggibile di ciascun annuncio.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 6%

---


# Nome annuncio

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Nome annuncio**. Per informazioni su come raccogliere questa variabile, consulta [Nome annuncio](/help/implementation/variables/ads/ad-name.md).*

>[!ENDSHADEBOX]

La dimensione **Nome annuncio** riporta il titolo leggibile di ciascun annuncio.

## Compilazione di questa dimensione

Il nome dell&#39;annuncio è impostato dal lettore a ogni evento [inizio annuncio](/help/implementation/events/ads/ad-start.md).

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.friendlyName` quando [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `videoadname`, `post_videoadname` |
| Audience Manager | `c_contextdata.a.media.ad.friendlyName` |

In Adobe Analytics, questa dimensione viene visualizzata in due modi: come **Nome annuncio (variabile)** (raccolto direttamente da `a.media.ad.friendlyName`) e come **Nome annuncio** (classificazione derivata dalla dimensione [Ad](ad.md)). Se utilizzi la classificazione, sei responsabile del popolamento e della manutenzione dei relativi valori utilizzando [Set di classificazione](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html). L&#39;utilizzo di **Nome annuncio (variabile)** non richiede alcuna manutenzione della classificazione, ma si perde la relazione 1:1 garantita tra il nome annuncio e la dimensione [Annuncio](ad.md) padre. Utilizza qualsiasi componente supportato maggiormente dal flusso di lavoro di implementazione.

## Elementi dimensionali

Ogni elemento rappresenta il titolo letterale dell&#39;annuncio riportato all&#39;[inizio annuncio](/help/implementation/events/ads/ad-start.md) (ad esempio, `"Ford F-150"`).
