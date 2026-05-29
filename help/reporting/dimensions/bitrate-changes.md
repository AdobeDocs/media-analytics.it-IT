---
title: Modifiche al bitrate (dimensione)
description: Segnala il conteggio degli eventi di modifica del bitrate per sessione.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 5%

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
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.bitrateChangeCount` quando [[!UICONTROL Media Quality]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `videoqoebitratechangecountevar`, `post_videoqoebitratechangecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

## Elementi dimensionali

Ogni elemento è il valore letterale del conteggio delle modifiche riportato nella chiamata di chiusura. Per il reporting booleano a livello di sessione (se la sessione ha subito una qualsiasi modifica del bitrate), utilizza [Flussi interessati dalla modifica del bitrate](/help/reporting/metrics/bitrate-change-impacted-streams.md).
