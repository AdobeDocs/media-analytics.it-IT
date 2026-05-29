---
title: Autore
description: Segnala l’autore del contenuto. Utilizzato principalmente per gli audiolibri.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 11%

---


# Autore

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Autore**. Per informazioni su come raccogliere questa variabile, vedere [Autore](/help/implementation/variables/standard-metadata/author.md).*

>[!ENDSHADEBOX]

La dimensione **Autore** segnala l&#39;autore del contenuto, ad esempio `"Eleanor Clementine"`. Utilizzato principalmente per gli audiolibri, ma valido anche per i podcast il cui host o produttore rappresenta l’attribuzione pertinente.

## Compilazione di questa dimensione

L’autore viene impostato dal lettore all’inizio della sessione per i contenuti audio.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.author` quando [[!UICONTROL Audio Metadata]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.author`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videoaudioauthor` |
| Audience Manager | `c_contextdata.a.media.author` |

## Elementi dimensionali

Ogni elemento rappresenta il nome dell’autore letterale riportato all’inizio della sessione.
