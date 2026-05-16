---
title: Stagione
description: Segnala il numero di stagione per i contenuti episodici.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 10%

---


# Stagione

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Stagione**. Consulta [Stagione](/help/implementation/variables/standard-metadata/season.md) per informazioni su come raccogliere questa variabile.*

>[!ENDSHADEBOX]

La dimensione **Stagione** riporta il numero della stagione per il contenuto episodico. Utilizzalo insieme a [Show](show.md) e [Episode](episode.md) per le interruzioni a episodi complete.

## Compilazione di questa dimensione

La stagione è impostata dal lettore all’inizio della sessione quando il contenuto fa parte di una serie.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.season` quando [[!UICONTROL Video Metadata]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.season`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoseason`, `post_videoseason` |
| Audience Manager | `c_contextdata.a.media.season` |

## Elementi dimensionali

Ogni elemento rappresenta il valore letterale della stagione riportato all&#39;inizio della sessione (in genere un numero intero di stringa come `"1"`, `"2"`). Essere coerente tra gli episodi all&#39;interno dello stesso spettacolo; la dimensione non normalizza `"1"` e `"01"` allo stesso elemento riga.
