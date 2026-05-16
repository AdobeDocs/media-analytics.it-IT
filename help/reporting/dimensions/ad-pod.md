---
title: Ad pod
description: Segnala ogni interruzione pubblicitaria univoca, codificata da un ID pod generato automaticamente.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 7%

---


# Ad pod

La dimensione **Ad pod** riporta ogni interruzione pubblicitaria univoca, segnalata da un ID pod generato automaticamente. Ogni annuncio in una sessione appartiene a un pod dell’annuncio principale, che raggruppa più annunci riprodotti uno dopo l’altro. Utilizza la dimensione per interrompere il coinvolgimento tramite interruzione pubblicitaria e come chiave di unione per le classificazioni [Pod name](pod-name.md) e [Pod position](pod-position.md).

## Compilazione di questa dimensione

L&#39;ID del pod dell&#39;annuncio viene generato automaticamente da SDK quando viene attivato un evento [inizio interruzione annuncio](/help/implementation/events/ads/ad-break-start.md). Le implementazioni API dirette costruiscono l’ID dall’indice di interruzione e dall’ora di inizio o forniscono un ID pod personalizzato.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.pod` quando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.advertisingPodDetails.ID`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Feed di dati | `videoadpod`, `post_videoadpod` |
| Audience Manager | N/D |

## Elementi dimensionali

Ogni elemento è un ID univoco dell’ad pod. L&#39;ID è opaco (in genere un hash di ID sessione, ID contenuto e indice di interruzione) ed è più utile come chiave di raggruppamento quando combinato con [Nome pod](pod-name.md) per l&#39;etichetta intuitiva.
