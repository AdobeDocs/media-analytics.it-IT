---
title: Album
description: Segnala l’album a cui appartiene la traccia audio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 9%

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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.album` quando [[!UICONTROL Audio Metadata]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.album`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoaudioalbum` |

## Elementi dimensionali

Ogni elemento rappresenta il titolo letterale dell’album riportato all’inizio della sessione. Due album con lo stesso titolo di artisti diversi vengono compressi in un&#39;unica riga. Accoppia con la dimensione [Artista](artist.md) per evitare ambiguità.
