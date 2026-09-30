---
title: Segmento di contenuto
description: Segnala l’intervallo della testina di riproduzione visualizzato durante una sessione, in minuti.
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
source-wordcount: '200'
ht-degree: 7%
---

# Segmento di contenuto

La dimensione **Segmento di contenuto** riporta l&#39;intervallo della testina di riproduzione visualizzato durante una sessione, in minuti (ad esempio, `[0-5]` per i minuti da 0 a 5). Il backend calcola il segmento dai valori minimi e massimi della testina di riproduzione riportati durante la riproduzione. Utilizzala insieme alla metrica [Visualizzazioni del segmento di contenuto](/help/reporting/metrics/content-segment-views.md) per analizzare quali parti dei visualizzatori di contenuto a lunga forma vengono effettivamente utilizzate.

## Compilazione di questa dimensione

Il segmento di contenuto viene calcolato dal backend multimediale in base ai valori della testina di riproduzione riportati negli eventi della sessione. Non è impostato dal client. Il valore riportato è derivato dai valori della testina di riproduzione visualizzati durante la riproduzione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.segment` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.segment`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videosegment`, `post_videosegment` |
| Audience Manager | `c_contextdata.a.media.segment` |

>[!IMPORTANT]
>
>Se la testina di riproduzione non viene riportata correttamente durante la sessione, il segmento calcolato potrebbe non essere accurato. Per i flussi live, il segmento viene calcolato dai relativi valori della testina di riproduzione visualizzati durante la sessione.

## Elementi dimensionali

Ogni elemento è un intervallo di stringhe che include i valori della testina di riproduzione visualizzati durante una sessione (ad esempio, `[0-5]`, `[5-10]`, `[10-15]`). La granularità è fissata a cinque minuti.
