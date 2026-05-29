---
title: URL creatività
description: Segnala l’URL della risorsa di ciascun annuncio creativo.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 10%

---


# URL creatività

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **URL Creative**. Per informazioni su come raccogliere questa variabile, vedere [URL Creative](/help/implementation/variables/ads/creative-url.md).*

>[!ENDSHADEBOX]

La dimensione **URL Creative** riporta l&#39;URL della risorsa di ciascun annuncio creativo. Utilizza la dimensione quando l’URL stesso è significativo per l’analisi (ad esempio, per distinguere i percorsi CDN o le versioni creative).

## Compilazione di questa dimensione

L&#39;URL di Creative viene impostato dal lettore a ogni evento [ad start](/help/implementation/events/ads/ad-start.md).

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Crea una [regola di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.ad.creativeURL` a un eVar. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l&#39;eVar a cui la regola di elaborazione mappa `a.media.ad.creativeURL`) |
| Audience Manager | `c_contextdata.a.media.ad.creativeURL` |

## Elementi dimensionali

Ogni elemento rappresenta la stringa dell&#39;URL letterale segnalata all&#39;[inizio annuncio](/help/implementation/events/ads/ad-start.md).
