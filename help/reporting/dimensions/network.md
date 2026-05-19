---
title: Rete
description: Segnala il nome della rete di trasmissione o del canale.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 11%

---


# Rete

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Rete**. Per informazioni su come raccogliere la variabile, vedere [Rete](/help/implementation/variables/standard-metadata/network.md).*

>[!ENDSHADEBOX]

La dimensione **Rete** riporta il nome della rete di trasmissione o del canale (ad esempio, `"Fox"` o `"ESPN"`). Utilizzalo per confrontare il coinvolgimento tra reti all’interno della stessa proprietà di streaming.

## Compilazione di questa dimensione

La rete viene impostata dal lettore all&#39;avvio della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.network` quando [[!UICONTROL Video Metadata]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.network`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videonetwork`, `post_videonetwork` |
| Audience Manager | `c_contextdata.a.media.network` |

## Elementi dimensionali

Ogni elemento rappresenta il valore di rete letterale riportato all&#39;avvio della sessione. Utilizza un nome distinto e stabile per rete in modo che i dati non si frammentino tra le varianti ortografiche.
