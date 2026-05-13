---
title: Artista
description: Segnala l’artista che esegue i contenuti audio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 9%

---


# Artista

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Artista**. Per informazioni su come raccogliere questa variabile, consulta [Artista](/help/implementation/variables/standard-metadata/artist.md).*

>[!ENDSHADEBOX]

La dimensione **Artista** segnala l&#39;artista che esegue l&#39;operazione per il contenuto audio (ad esempio, `"Crested Larks"`). Utilizzalo per dare inizio al coinvolgimento su musica o cataloghi podcast da parte dell&#39;esecutore.

## Compilazione di questa dimensione

L&#39;artista è impostato dal lettore all&#39;inizio della sessione per il contenuto audio.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.artist` quando [[!UICONTROL Audio Metadata]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.artist`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoaudioartist` |

## Elementi dimensionali

Ogni elemento rappresenta il nome letterale dell’artista riportato all’inizio della sessione. Utilizza un nome stabile e canonico per artista in modo che i dati non si frammentino tra le varianti di formattazione.
