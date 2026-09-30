---
title: Ad pod
description: Segnala ogni interruzione pubblicitaria univoca, codificata da un ID pod generato automaticamente.
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
source-wordcount: '195'
ht-degree: 8%
---

# Ad pod

La dimensione **Ad pod** riporta ogni interruzione pubblicitaria univoca, segnalata da un ID pod generato automaticamente. Ogni annuncio in una sessione appartiene a un pod dell’annuncio principale, che raggruppa più annunci riprodotti uno dopo l’altro. Utilizza la dimensione per interrompere il coinvolgimento tramite interruzione pubblicitaria e come chiave di unione per le classificazioni [Pod name](pod-name.md) e [Pod position](pod-position.md).

## Compilazione di questa dimensione

L&#39;ID del pod dell&#39;annuncio viene generato automaticamente da SDK quando viene attivato un evento [inizio interruzione annuncio](/help/implementation/events/ads/ad-break-start.md). Le implementazioni API dirette costruiscono l’ID dall’indice di interruzione e dall’ora di inizio o forniscono un ID pod personalizzato.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.pod` quando [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.ID`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Feed di dati | `videoadpod`, `post_videoadpod` |
| Audience Manager | N/D |

## Elementi dimensionali

Ogni elemento è un ID univoco dell’ad pod. L&#39;ID è opaco (in genere un hash di ID sessione, ID contenuto e indice di interruzione) ed è più utile come chiave di raggruppamento quando combinato con [Nome pod](pod-name.md) per l&#39;etichetta intuitiva.
