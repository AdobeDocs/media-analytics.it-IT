---
title: Bitrate medio (dimensione)
description: Segnala il bitrate medio a blocchi di ciascuna sessione a intervalli di 100 kbps.
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
ht-degree: 8%
---

# Bitrate medio (dimensione)

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la dimensione **Bitrate medio**, che indica il bitrate a blocchi di ogni sessione. Vedi [Bitrate medio (metrica)](/help/reporting/metrics/average-bitrate.md) per la metrica della media ponderata non elaborata. Per informazioni su come raccogliere questa variabile, consulta [Bitrate](/help/implementation/variables/quality/bitrate.md).*

>[!ENDSHADEBOX]

La dimensione **Velocità in bit media** riporta la velocità in bit media di riproduzione per sessione, inserita in intervalli di 100 kbps. Il backend calcola il valore come media ponderata di tutti i valori del bitrate nella sessione, quindi lo assegna a un bucket. Utilizza la dimensione per suddividere coinvolgimento e qualità per livello bitrate.

## Compilazione di questa dimensione

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.bitrateAverageBucket` quando [[!UICONTROL Media Quality]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateAverageBucket`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `videoqoebitrateaverageevar`, `post_videoqoebitrateaverageevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateAverageBucket` |

## Elementi dimensionali

Ogni elemento è un&#39;etichetta di bucket bitrate (ad esempio, `800-899`, `3200-3299`). Utilizza il [bitrate medio (metrica)](/help/reporting/metrics/average-bitrate.md) per un valore medio ponderato non elaborato, anziché per una dimensione a blocchi.
