---
title: Nome annuncio
description: Riporta il titolo leggibile di ciascun annuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 5%

---


# Nome annuncio

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Nome annuncio**. Per informazioni su come raccogliere questa variabile, consulta [Nome annuncio](/help/implementation/variables/ads/ad-name.md).*

>[!ENDSHADEBOX]

La dimensione **Nome annuncio** riporta il titolo leggibile di ciascun annuncio.

## Compilazione di questa dimensione

Il nome dell&#39;annuncio viene impostato dal lettore a ogni evento `media.adStart`.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.friendlyName` quando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.friendlyName`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `videoadname, post_videoadname` |

In Adobe Analytics, questa dimensione viene visualizzata in due modi: come **Nome annuncio (variabile)** (raccolto direttamente da `a.media.ad.friendlyName`) e come **Nome annuncio** (classificazione derivata dalla dimensione [Ad](ad.md)). Se utilizzi la classificazione, sei responsabile del popolamento e della manutenzione dei relativi valori utilizzando [Set di classificazione](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html). L&#39;utilizzo di **Nome annuncio (variabile)** non richiede alcuna manutenzione della classificazione, ma si perde la relazione 1:1 garantita tra il nome annuncio e la dimensione [Annuncio](ad.md) padre. Utilizza qualsiasi componente supportato maggiormente dal flusso di lavoro di implementazione.

## Elementi dimensionali

Ogni elemento rappresenta il titolo dell&#39;annuncio letterale riportato su `media.adStart` (ad esempio, `"Ford F-150"`).
