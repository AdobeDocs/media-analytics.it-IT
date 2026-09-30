---
title: ID errore SDK del lettore
description: Segnala identificatori di errore univoci generati dal lettore di contenuti SDK.
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

# ID errore SDK del lettore

La dimensione **ID errore SDK del lettore** riporta identificatori di errore univoci generati dal SDK del lettore di contenuti durante una sessione. Il lettore deve fornire i codici o gli ID al momento dell’implementazione tramite l’API di tracciamento degli errori. Sono supportati più ID di errore per sessione.

## Compilazione di questa dimensione

Il lettore trasmette gli ID di errore del lettore-SDK al tracker per [errori](/help/implementation/events/error.md) eventi. Il backend raccoglie ID univoci in tutta la sessione e li segnala nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.playerSdkErrors` quando [[!UICONTROL Media Quality]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.playerSdkErrors`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `videoqoeplayersdkerrors`, `post_videoqoeplayersdkerrors` |
| Audience Manager | `c_contextdata.a.media.qoe.playerSdkErrors` |

## Elementi dimensionali

Ogni elemento è un codice di errore o un ID generato dal lettore SDK. Utilizza una tassonomia stabile tra le implementazioni in modo che gli ID di errore vengano aggregati correttamente tra le sessioni.
