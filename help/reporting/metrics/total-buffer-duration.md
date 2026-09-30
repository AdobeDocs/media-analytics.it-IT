---
title: Durata totale del buffer (metrica)
description: Segnala il tempo di buffer cumulativo per somme e medie tra sessioni.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 7%
---

# Durata totale del buffer (metrica)

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica **Durata totale buffer**. Adobe Analytics compila automaticamente una [durata totale del buffer (dimensione)](/help/reporting/dimensions/total-buffer-duration.md) associata dalla stessa variabile di dati di contesto `a.media.qoe.bufferTime`. Customer Journey Analytics espone un singolo campo `xdm.mediaReporting.qoeDataDetails.bufferTime` che è possibile utilizzare come dimensione o come metrica.*

>[!ENDSHADEBOX]

La metrica **Durata totale buffer** riporta il tempo di buffer cumulativo tra le sessioni, adatto a somme, medie e aggregazioni percentili. Utilizza la metrica per calcolare il tempo totale trascorso dai clienti in attesa sui buffer in un periodo di rapporto.

## Come è calcolata questa metrica

Il backend del supporto somma la durata di ogni intervallo di buffer (da [inizio buffer](/help/implementation/events/playback/buffer-start.md) alla successiva modifica dello stato). La metrica viene segnalata nella chiamata di chiusura. Analysis Workspace mostra il valore come `HH:MM:SS`; Feed dati, Data Warehouse e API di reporting mostrano il valore in secondi.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.bufferTime` quando [[!UICONTROL Media Quality]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.bufferTime` |
