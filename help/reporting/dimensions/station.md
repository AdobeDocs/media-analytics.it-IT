---
title: Stazione
description: Segnala il nome o l'ID della stazione radio per il contenuto della trasmissione audio.
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
source-wordcount: '136'
ht-degree: 10%
---

# Stazione

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Stazione**. Per informazioni su come raccogliere questa variabile, vedere [Stazione](/help/implementation/variables/standard-metadata/station.md).*

>[!ENDSHADEBOX]

La dimensione **Stazione** riporta il nome o l&#39;ID della stazione radio che trasmette il contenuto audio (ad esempio, `"NPR"` o `"WXYZ-FM"`). Utilizzalo per confrontare il coinvolgimento tra le stazioni in una rete sindacata.

## Compilazione di questa dimensione

La stazione viene impostata dal lettore all&#39;inizio della sessione per il contenuto audio.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.station` quando [[!UICONTROL Audio Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.station`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoaudiostation` |
| Audience Manager | `c_contextdata.a.media.station` |

## Elementi dimensionali

Ogni elemento rappresenta il nome o l&#39;ID letterale della stazione segnalato all&#39;inizio della sessione. Utilizza un singolo identificatore canonico per stazione in modo che il coinvolgimento non si frammenti tra le varianti di segnale di chiamata.
