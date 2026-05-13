---
title: Segmento di contenuto
description: Segnala l’intervallo della testina di riproduzione visualizzato durante una sessione, in minuti.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 5%

---


# Segmento di contenuto

La dimensione **Segmento di contenuto** riporta l&#39;intervallo della testina di riproduzione visualizzato durante una sessione, in minuti (ad esempio, `[0-5]` per i minuti da 0 a 5). Il backend calcola il segmento dai valori minimi e massimi della testina di riproduzione riportati durante la riproduzione. Utilizzala insieme alla metrica [Visualizzazioni del segmento di contenuto](/help/reporting/metrics/content-segment-views.md) per analizzare quali parti dei visualizzatori di contenuto a lunga forma vengono effettivamente utilizzate.

## Compilazione di questa dimensione

Il segmento di contenuto viene calcolato dal backend multimediale in base ai valori della testina di riproduzione riportati negli eventi della sessione. Non è impostato dal client. Il valore riportato è derivato dai valori della testina di riproduzione visualizzati durante la riproduzione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.segment` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.segment`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videosegment, post_videosegment` |

>[!IMPORTANT]
>
>Se la testina di riproduzione non viene riportata correttamente durante la sessione, il segmento calcolato potrebbe non essere accurato. Per i flussi live, il segmento viene calcolato dai relativi valori della testina di riproduzione visualizzati durante la sessione.

## Elementi dimensionali

Ogni elemento è un intervallo di stringhe che include i valori della testina di riproduzione visualizzati durante una sessione (ad esempio, `[0-5]`, `[5-10]`, `[10-15]`). La granularità è fissata a cinque minuti.
