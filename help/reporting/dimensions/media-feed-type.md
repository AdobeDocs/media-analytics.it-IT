---
title: Tipo di feed multimediale
description: Segnala il feed del broadcast (ad esempio, East-HD o West-SD) quando lo stesso contenuto viene distribuito tramite più feed.
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
source-wordcount: '157'
ht-degree: 8%
---

# Tipo di feed multimediale

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Tipo di feed multimediale**. Per informazioni su come raccogliere questa variabile, vedere [Tipo di feed multimediale](/help/implementation/variables/standard-metadata/media-feed-type.md).*

>[!ENDSHADEBOX]

La dimensione **Tipo di feed multimediale** riporta il feed di trasmissione per ogni sessione (ad esempio, `"East-HD"`, `"West-SD"` o `"4K"`). Utilizzalo quando lo stesso contenuto viene distribuito tramite più feed regionali o di qualità e il coinvolgimento deve essere segnalato per feed.

## Compilazione di questa dimensione

Il tipo di feed multimediale viene impostato dal lettore all’inizio della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.feed` quando [[!UICONTROL Video Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.feed`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videofeedtype`, `post_videofeedtype` |
| Audience Manager | `c_contextdata.a.media.feed` |

## Elementi dimensionali

Ogni elemento rappresenta il valore di feed letterale riportato all’inizio della sessione. Utilizza un set stabile di identificatori dei mangimi per suddivisione regionale o di qualità.
