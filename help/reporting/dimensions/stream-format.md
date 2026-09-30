---
title: Formato flusso
description: Segnala il livello di qualità di ciascuna sessione (tipicamente HD o SD).
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
