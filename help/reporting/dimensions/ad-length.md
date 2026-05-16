---
title: Lunghezza annuncio
description: Segnala la durata in secondi di ciascun annuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 8%

---


# Lunghezza annuncio

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Lunghezza annuncio**. Per informazioni su come raccogliere questa variabile, consulta [Lunghezza annuncio](/help/implementation/variables/ads/ad-length.md).*

>[!ENDSHADEBOX]

La dimensione **Lunghezza annuncio** riporta la durata in secondi di ciascun annuncio.

## Compilazione di questa dimensione

La lunghezza dell&#39;annuncio è impostata dal lettore a ogni evento [inizio annuncio](/help/implementation/events/ads/ad-start.md).

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.length` quando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.length`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `videoadlength`, `post_videoadlength` |
| Audience Manager | `c_contextdata.a.media.ad.length` |

In Adobe Analytics, questa dimensione viene visualizzata in due modi: come **Lunghezza annuncio (variabile)** (raccolta direttamente da `a.media.ad.length`) e come **Lunghezza annuncio** (classificazione derivata dalla dimensione [Ad](ad.md)). Se utilizzi la classificazione, sei responsabile del popolamento e della manutenzione dei relativi valori utilizzando [Set di classificazione](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html). L&#39;utilizzo di **Lunghezza annuncio (variabile)** non richiede alcuna manutenzione della classificazione, ma si perde la relazione 1:1 garantita tra la lunghezza dell&#39;annuncio e la dimensione [Ad](ad.md) padre. Utilizza qualsiasi componente supportato maggiormente dal flusso di lavoro di implementazione.

## Elementi dimensionali

Ogni elemento rappresenta il valore letterale della lunghezza dell&#39;annuncio, in secondi, segnalato all&#39;[inizio annuncio](/help/implementation/events/ads/ad-start.md).
