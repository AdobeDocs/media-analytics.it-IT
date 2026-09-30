---
title: Rete
description: Segnala il nome della rete di trasmissione o del canale.
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
source-wordcount: '125'
ht-degree: 12%
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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.network` quando [[!UICONTROL Video Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.network`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videonetwork`, `post_videonetwork` |
| Audience Manager | `c_contextdata.a.media.network` |

## Elementi dimensionali

Ogni elemento rappresenta il valore di rete letterale riportato all&#39;avvio della sessione. Utilizza un nome distinto e stabile per rete in modo che i dati non si frammentino tra le varianti ortografiche.
