---
title: Tempo di avvio (metrica)
description: Segnala il tempo di avvio per somme e medie tra sessioni.
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
source-wordcount: '200'
ht-degree: 7%
---

# Tempo di avvio (metrica)

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica **Tempo di avvio**. Adobe Analytics compila automaticamente un [tempo di avvio (dimensione)](/help/reporting/dimensions/time-to-start.md) associato dalla stessa variabile di dati di contesto `a.media.qoe.timeToStart`. Customer Journey Analytics espone un singolo campo `xdm.mediaReporting.qoeDataDetails.timeToStart` che è possibile utilizzare come dimensione o come metrica. Vedi [Ora di inizio](/help/implementation/variables/quality/time-to-start.md) per informazioni su come raccogliere questa variabile.*

>[!ENDSHADEBOX]

La metrica **Tempo di avvio** indica il tempo di avvio tra le sessioni, adatto a somme, medie e aggregazioni percentili. Utilizza la metrica per calcolare il tempo medio di avvio in un periodo di report e confrontare le prestazioni di avvio tra contenuti, reti o lettori. Adobe memorizza il valore in secondi e converte al momento dell’acquisizione dai millisecondi riportati dal lettore.

## Come è calcolata questa metrica

Il lettore imposta `timeToStart` sull&#39;oggetto QoE prima dell&#39;avvio della sessione. Il backend riporta il valore nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.timeToStart` quando [[!UICONTROL Media Quality]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |
