---
title: Eventi buffer (dimensione)
description: Riporta il numero di eventi di buffering per sessione.
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
source-wordcount: '173'
ht-degree: 8%
---

# Eventi buffer (dimensione)

>[!BEGINSHADEBOX]

*In questa pagina sono inclusi **eventi buffer**. Adobe Analytics compila automaticamente un [evento buffer (metrica)](/help/reporting/metrics/buffer-events.md) associato dalla stessa variabile di dati di contesto `a.media.qoe.bufferCount`. Customer Journey Analytics espone un singolo campo `xdm.mediaReporting.qoeDataDetails.bufferCount` che è possibile utilizzare come dimensione o come metrica.*

>[!ENDSHADEBOX]

La dimensione **Eventi buffer** riporta il conteggio degli eventi di buffering che si sono verificati durante una sessione. Utilizza la dimensione per suddividere il coinvolgimento in base al numero esatto di buffer.

## Compilazione di questa dimensione

Il backend multimediale incrementa il conteggio ogni volta che il lettore entra in uno stato `buffer`. Il valore viene segnalato nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.bufferCount` quando [[!UICONTROL Media Quality]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `videoqoebuffercountevar`, `post_videoqoebuffercountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

## Elementi dimensionali

Ogni elemento è il valore letterale del conteggio dei buffer riportato nella chiamata di chiusura. Per il reporting booleano a livello di sessione (se la sessione ha riscontrato un buffering), utilizza [Flussi interessati dal buffer](/help/reporting/metrics/buffer-impacted-streams.md).
