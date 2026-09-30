---
title: Album
description: Segnala l’album a cui appartiene la traccia audio.
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
source-wordcount: '134'
ht-degree: 10%
---

# Album

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Album**. Per informazioni su come raccogliere questa variabile, vedere [Album](/help/implementation/variables/standard-metadata/album.md).*

>[!ENDSHADEBOX]

La dimensione **Album** indica l&#39;album a cui appartiene il brano audio (ad esempio, `"Pinegrove"`). Utilizzarlo per eseguire il rollup dei brani dello stesso album.

## Compilazione di questa dimensione

L&#39;album viene impostato dal lettore all&#39;inizio della sessione per il contenuto audio.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.album` quando [[!UICONTROL Audio Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.album`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoaudioalbum` |
| Audience Manager | `c_contextdata.a.media.album` |

## Elementi dimensionali

Ogni elemento rappresenta il titolo letterale dell’album riportato all’inizio della sessione. Due album con lo stesso titolo di artisti diversi vengono compressi in un&#39;unica riga. Accoppia con la dimensione [Artista](artist.md) per evitare ambiguità.
