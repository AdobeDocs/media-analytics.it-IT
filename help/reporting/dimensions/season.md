---
title: Stagione
description: Segnala il numero di stagione per i contenuti episodici.
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
source-wordcount: '138'
ht-degree: 11%
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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.season` quando [[!UICONTROL Video Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.season`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoseason`, `post_videoseason` |
| Audience Manager | `c_contextdata.a.media.season` |

## Elementi dimensionali

Ogni elemento rappresenta il valore letterale della stagione riportato all&#39;inizio della sessione (in genere un numero intero di stringa come `"1"`, `"2"`). Essere coerente tra gli episodi all&#39;interno dello stesso spettacolo; la dimensione non normalizza `"1"` e `"01"` allo stesso elemento riga.
