---
title: Episodio
description: Riporta il numero dell’episodio in una stagione.
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
source-wordcount: '130'
ht-degree: 12%
---

# Episodio

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Episodio**. Vedi [Episodio](/help/implementation/variables/standard-metadata/episode.md) per informazioni su come raccogliere questa variabile.*

>[!ENDSHADEBOX]

La dimensione **Episodio** riporta il numero di episodio in una stagione. Utilizzalo insieme a [Show](show.md) e [Season](season.md) per interrompere il coinvolgimento a livello del singolo episodio.

## Compilazione di questa dimensione

L’episodio viene impostato dal lettore all’inizio della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.episode` quando [[!UICONTROL Video Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.episode`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoepisode`, `post_videoepisode` |
| Audience Manager | `c_contextdata.a.media.episode` |

## Elementi dimensionali

Ogni elemento rappresenta il valore letterale dell&#39;episodio segnalato all&#39;inizio della sessione (in genere un numero intero di stringa come `"13"`). I numeri degli episodi da soli non sono univoci nelle stagioni; abbina con Stagione per breakout non ambigui.
