---
title: Nome del lettore dell’annuncio
description: Segnala quale lettore ha eseguito il rendering di ciascun annuncio.
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
source-wordcount: '132'
ht-degree: 10%
---

# Nome del lettore dell’annuncio

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Nome del lettore dell&#39;annuncio**. Per informazioni su come raccogliere questa variabile, consulta [Il nome del lettore dell&#39;annuncio](/help/implementation/variables/ads/ad-player-name.md).*

>[!ENDSHADEBOX]

La dimensione **Nome del lettore dell&#39;annuncio** riporta il rendering di ciascun annuncio eseguito dal lettore (ad esempio, `"Freewheel"`, `"Google IMA"`). Il lettore di annunci può differire dal lettore di contenuto principale quando gli annunci sono uniti da un servizio di inserimento di annunci lato server.

## Compilazione di questa dimensione

Il nome del lettore dell&#39;annuncio è impostato dal lettore a ogni evento [inizio annuncio](/help/implementation/events/ads/ad-start.md).

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.playerName` quando [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `videoadplayername`, `post_videoadplayername` |
| Audience Manager | `c_contextdata.a.media.ad.playerName` |

## Elementi dimensionali

Ogni elemento rappresenta il nome letterale del lettore di annunci riportato all&#39;[inizio annuncio](/help/implementation/events/ads/ad-start.md).
