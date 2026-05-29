---
title: Formato flusso
description: Segnala il livello di qualità di ciascuna sessione (tipicamente HD o SD).
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 9%

---


# Formato flusso

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Formato flusso**. Per informazioni su come raccogliere la variabile, vedere [Formato flusso](/help/implementation/variables/standard-metadata/stream-format.md).*

>[!ENDSHADEBOX]

La dimensione **Formato flusso** riporta il livello di qualità di ogni sessione (in genere `"HD"` o `"SD"`, ma qualsiasi stringa è accettata). Puoi utilizzarlo per confrontare coinvolgimento, completamento e qualità tra i livelli di qualità della consegna.

## Compilazione di questa dimensione

Il formato del flusso viene impostato dal lettore all’inizio della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.format` a un eVar. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.streamFormat`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l&#39;eVar a cui la regola di elaborazione mappa `a.media.format`) |
| Audience Manager | `c_contextdata.a.media.format` |

## Elementi dimensionali

Ogni elemento rappresenta il valore del formato letterale riportato all’inizio della sessione. Utilizzare un set stabile di valori (`HD`, `SD`, `4K`, `UHD`) in modo che gli elementi di riga non si frammentino tra le varianti ortografiche.
