---
title: Artista
description: Segnala l’artista che esegue i contenuti audio.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 11%

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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.artist` quando [[!UICONTROL Audio Metadata]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.artist`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoaudioartist` |
| Audience Manager | `c_contextdata.a.media.artist` |

## Elementi dimensionali

Ogni elemento rappresenta il nome letterale dell’artista riportato all’inizio della sessione. Utilizza un nome stabile e canonico per artista in modo che i dati non si frammentino tra le varianti di formattazione.
