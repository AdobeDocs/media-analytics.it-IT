---
title: ID errore esterni
description: Segnala identificatori di errore univoci provenienti da origini esterne, ad esempio errori CDN.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 7%

---


# ID errore esterni

La dimensione **ID errore esterni** riporta identificatori di errore univoci da qualsiasi origine esterna al SDK del lettore (ad esempio, errori CDN). Il lettore deve fornire i codici o gli ID al momento dell’implementazione tramite l’API di tracciamento degli errori. Sono supportati più ID di errore per sessione.

## Compilazione di questa dimensione

Il lettore trasmette gli ID di errore esterni al tracker per [errori](/help/implementation/events/error.md) eventi. Il backend raccoglie ID univoci in tutta la sessione e li segnala nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.externalErrors` quando [[!UICONTROL Media Quality]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.externalErrors`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `videoqoeextneralerrors` |
| Audience Manager | `c_contextdata.a.media.qoe.externalErrors` |

## Elementi dimensionali

Ogni elemento è un codice di errore o un ID fornito dal lettore. Utilizza una tassonomia stabile tra le implementazioni in modo che gli ID di errore vengano aggregati correttamente tra le sessioni.
