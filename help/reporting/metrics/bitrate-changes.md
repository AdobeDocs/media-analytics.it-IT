---
title: Modifiche al bitrate (metrica)
description: Conta gli eventi di modifica del bitrate per somme e medie tra sessioni.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 7%

---


# Modifiche al bitrate (metrica)

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica **Modifiche bitrate**. Adobe Analytics compila automaticamente una coppia di [modifiche del bitrate (dimensione)](/help/reporting/dimensions/bitrate-changes.md) dalla stessa variabile di dati di contesto `a.media.qoe.bitrateChangeCount`. Customer Journey Analytics espone un singolo campo `xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` che è possibile utilizzare come dimensione o come metrica. Consulta [Modifica bitrate](/help/implementation/variables/quality/bitrate-change.md) per informazioni su come attivare gli eventi di modifica bitrate.*

>[!ENDSHADEBOX]

La metrica **Modifiche del bitrate** conta gli eventi di modifica del bitrate nelle sessioni, adatti a somme, medie e aggregazioni percentili. Utilizza la metrica per calcolare il volume totale delle modifiche del bitrate in un periodo di report e confrontare la stabilità del bitrate tra contenuti, reti o lettori.

## Come è calcolata questa metrica

Il backend multimediale incrementa il conteggio su ogni [evento di modifica del bitrate](/help/implementation/events/playback/bitrate-change.md) ricevuto durante la sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.bitrateChangeCount` quando [[!UICONTROL Media Quality]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

Per il reporting booleano a livello di sessione (se la sessione ha subito una qualsiasi modifica del bitrate), utilizza [Flussi interessati dalla modifica del bitrate](bitrate-change-impacted-streams.md).
