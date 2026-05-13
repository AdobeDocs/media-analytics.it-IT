---
title: Bitrate medio (dimensione)
description: Segnala il bitrate medio a blocchi di ciascuna sessione a intervalli di 100 kbps.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 6%

---


# Bitrate medio (dimensione)

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la dimensione **Bitrate medio**, che indica il bitrate a blocchi di ogni sessione. Vedi [Bitrate medio (metrica)](/help/reporting/metrics/average-bitrate.md) per la metrica della media ponderata non elaborata. Per informazioni su come raccogliere questa variabile, consulta [Bitrate](/help/implementation/variables/quality/bitrate.md).*

>[!ENDSHADEBOX]

La dimensione **Velocità in bit media** riporta la velocità in bit media di riproduzione per sessione, inserita in intervalli di 100 kbps. Il backend calcola il valore come media ponderata di tutti i valori del bitrate nella sessione, quindi lo assegna a un bucket. Utilizza la dimensione per suddividere coinvolgimento e qualità per livello bitrate.

## Compilazione di questa dimensione

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.bitrateAverageBucket` quando [[!UICONTROL Media Quality]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateAverageBucket`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `videoqoebitrateaverageevar, post_videoqoebitrateaverageevar` |

## Elementi dimensionali

Ogni elemento è un&#39;etichetta di bucket bitrate (ad esempio, `800-899`, `3200-3299`). Utilizza il [bitrate medio (metrica)](/help/reporting/metrics/average-bitrate.md) per un valore medio ponderato non elaborato, anziché per una dimensione a blocchi.
