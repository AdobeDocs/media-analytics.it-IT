---
title: Annuncio
description: Segnala ogni annuncio univoco riprodotto, identificato dall’ID annuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 7%

---


# Annuncio

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Ad**. Consulta [ID annuncio](/help/implementation/variables/ads/ad-id.md) per informazioni su come raccogliere questa variabile.*

>[!ENDSHADEBOX]

La dimensione **Ad** riporta ogni annuncio univoco riprodotto, identificato dall&#39;ID annuncio impostato all&#39;[inizio annuncio](/help/implementation/events/ads/ad-start.md). La dimensione è il raggruppamento principale per i rapporti sugli annunci e la chiave di unione per le classificazioni a livello di annuncio come Nome annuncio, Lunghezza annuncio e Creative ID.

## Compilazione di questa dimensione

L&#39;annuncio viene impostato dal lettore a ogni evento [ad start](/help/implementation/events/ads/ad-start.md) come identificatore stabile dell&#39;annuncio.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.ad.name` quando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) è abilitato. Persiste per la durata della visita. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.name`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `videoad`, `post_videoad` |
| Audience Manager | `c_contextdata.a.media.ad.name` |

>[!IMPORTANT]
>
>È necessario specificare l’ID dell’annuncio. Se non è impostato o è vuoto, l’annuncio viene eliminato dal reporting degli annunci multimediali in streaming.

## Elementi dimensionali

Ogni elemento è un ID annuncio univoco segnalato al [inizio annuncio](/help/implementation/events/ads/ad-start.md). Utilizza un identificatore stabile per creatività in modo che lo stesso annuncio venga aggregato a un singolo elemento nelle varie sessioni.
