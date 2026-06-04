---
title: Episodio
description: Riporta il numero dell’episodio in una stagione.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 10%

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
