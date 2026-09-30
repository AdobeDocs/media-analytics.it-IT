---
title: Modifiche al bitrate (dimensione)
description: Segnala il conteggio degli eventi di modifica del bitrate per sessione.
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
source-wordcount: '203'
ht-degree: 6%
---

# Modifiche al bitrate (dimensione)

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la dimensione **Modifiche al bitrate**. Adobe Analytics compila automaticamente una coppia di [modifiche del bitrate (metrica)](/help/reporting/metrics/bitrate-changes.md) dalla stessa variabile di dati di contesto `a.media.qoe.bitrateChangeCount`. Customer Journey Analytics espone un singolo campo `xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` che è possibile utilizzare come dimensione o come metrica. Consulta [Modifica bitrate](/help/implementation/variables/quality/bitrate-change.md) per informazioni su come attivare gli eventi di modifica bitrate.*

>[!ENDSHADEBOX]

La dimensione **Modifiche bitrate** riporta il conteggio degli eventi di modifica del bitrate che si sono verificati durante una sessione. Utilizza la dimensione per suddividere coinvolgimento e qualità in base al valore esatto del conteggio delle modifiche (ad esempio, &quot;sessioni con 3 modifiche del bitrate rispetto a sessioni con 0&quot;).

## Compilazione di questa dimensione

Il backend multimediale incrementa il conteggio su ogni [evento di modifica del bitrate](/help/implementation/events/playback/bitrate-change.md) ricevuto durante la sessione. Il valore viene segnalato nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.bitrateChangeCount` quando [[!UICONTROL Media Quality]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `videoqoebitratechangecountevar`, `post_videoqoebitratechangecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

## Elementi dimensionali

Ogni elemento è il valore letterale del conteggio delle modifiche riportato nella chiamata di chiusura. Per il reporting booleano a livello di sessione (se la sessione ha subito una qualsiasi modifica del bitrate), utilizza [Flussi interessati dalla modifica del bitrate](/help/reporting/metrics/bitrate-change-impacted-streams.md).
