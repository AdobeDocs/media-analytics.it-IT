---
title: Album
description: Segnala l’album a cui appartiene la traccia audio.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
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
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.album`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoaudioalbum` |
| Audience Manager | `c_contextdata.a.media.album` |

## Elementi dimensionali

Ogni elemento rappresenta il titolo letterale dell’album riportato all’inizio della sessione. Due album con lo stesso titolo di artisti diversi vengono compressi in un&#39;unica riga. Accoppia con la dimensione [Artista](artist.md) per evitare ambiguità.
