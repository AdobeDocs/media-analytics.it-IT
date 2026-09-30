---
title: Capitolo
description: Segnala ogni capitolo univoco riprodotto, codificato da un ID capitolo generato automaticamente.
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
source-wordcount: '194'
ht-degree: 9%
---

# Capitolo

La dimensione **Capitolo** riporta ogni capitolo univoco riprodotto, codificato da un ID capitolo generato automaticamente. L’ID è costruito da SDK o dal back-end dall’ID contenuto, dall’indice del capitolo e dall’ora di inizio del capitolo. Pertanto, due sessioni dello stesso capitolo sullo stesso contenuto vengono aggregate a una singola riga. Utilizza la dimensione come chiave di unione per le classificazioni a livello di capitolo, ad esempio Nome capitolo, Lunghezza capitolo, Offset capitolo e Posizione capitolo.

## Compilazione di questa dimensione

L&#39;ID del capitolo viene generato automaticamente quando viene attivato un evento [inizio capitolo](/help/implementation/events/chapters/chapter-start.md). Il valore non viene impostato direttamente, ma deriva dalla posizione del capitolo, dall&#39;offset e dall&#39;ID contenuto.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.chapter.name` quando [[!UICONTROL Media Chapters]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feed di dati | `videochapter`, `post_videochapter` |
| Audience Manager | N/D |

## Elementi dimensionali

Ogni elemento è un ID capitolo univoco. L’ID è opaco (in genere un hash di ID contenuto + indice + offset) ed è più utile come chiave di raggruppamento. Accoppia con [Nome capitolo](chapter-name.md) per un&#39;etichetta intuitiva.
