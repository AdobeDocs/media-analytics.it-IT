---
title: Capitolo
description: Segnala ogni capitolo univoco riprodotto, codificato da un ID capitolo generato automaticamente.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 6%

---


# Capitolo

La dimensione **Capitolo** riporta ogni capitolo univoco riprodotto, codificato da un ID capitolo generato automaticamente. L’ID è costruito da SDK o dal back-end dall’ID contenuto, dall’indice del capitolo e dall’ora di inizio del capitolo. Pertanto, due sessioni dello stesso capitolo sullo stesso contenuto vengono aggregate a una singola riga. Utilizza la dimensione come chiave di unione per le classificazioni a livello di capitolo, ad esempio Nome capitolo, Lunghezza capitolo, Offset capitolo e Posizione capitolo.

## Compilazione di questa dimensione

L&#39;ID del capitolo viene generato automaticamente quando `media.chapterStart` viene attivato. Il valore non viene impostato direttamente, ma deriva dalla posizione del capitolo, dall&#39;offset e dall&#39;ID contenuto.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.chapter.name` quando [[!UICONTROL Media Chapters]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feed di dati | `videochapter, post_videochapter` |

## Elementi dimensionali

Ogni elemento è un ID capitolo univoco. L’ID è opaco (in genere un hash di ID contenuto + indice + offset) ed è più utile come chiave di raggruppamento. Accoppia con [Nome capitolo](chapter-name.md) per un&#39;etichetta intuitiva.
