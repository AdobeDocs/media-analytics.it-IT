---
title: Tempo trascorso dei contenuti
description: Segnala i secondi totali di riproduzione dei contenuti principali attivi per sessione.
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
source-wordcount: '219'
ht-degree: 6%
---

# Tempo trascorso dei contenuti

La metrica **Tempo contenuto trascorso** riporta i secondi totali di riproduzione del contenuto principale attivo per sessione, esclusi annunci, pause, buffering e blocchi. Utilizzala come metrica di coinvolgimento per la visualizzazione dei contenuti; per il tempo trascorso, inclusi gli annunci, consulta [Tempo trascorso sui contenuti multimediali](media-time-spent.md).

## Come è calcolata questa metrica

Il backend multimediale somma il tempo wall-clock trascorso tra gli eventi mentre il lettore è nello stato `play` sul contenuto principale. È escluso il tempo durante annunci, pause, eventi buffer e blocchi. Poiché viene conteggiato solo il tempo di riproduzione attivo, la metrica può superare [la lunghezza del contenuto](/help/reporting/dimensions/content-length.md) quando un visualizzatore cerca all&#39;indietro e guarda nuovamente un segmento. Ogni passaggio attraverso un dato segmento accumula un tempo di riproduzione aggiuntivo e può durare finché l’utente consuma e riavvolge il contenuto in una sessione. La metrica viene segnalata nella chiamata di chiusura. Il valore viene visualizzato come `HH:MM:SS` in Analysis Workspace e in secondi in Feed dati, Data Warehouse e API di reporting.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.timePlayed` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.timePlayed`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.timePlayed` |
