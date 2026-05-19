---
title: Flussi interessati dalla funzione sottotitoli
description: Conta le sessioni in cui il visualizzatore ha abilitato i sottotitoli almeno una volta.
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 8%

---


# Flussi interessati dalla funzione sottotitoli

>[!BEGINSHADEBOX]

*In questa pagina sono descritti i **Flussi interessati dalla metrica di generazione rapporti sottotitoli**. Vedi [Sottotitoli](/help/implementation/variables/player-state/closed-captioning.md) per informazioni su come raccogliere questa variabile.*

>[!ENDSHADEBOX]

La metrica **Flussi interessati dai sottotitoli** conta le sessioni in cui il visualizzatore ha abilitato i sottotitoli almeno una volta. La metrica è un valore booleano a livello di sessione: più sottotitoli vengono alternati, all’interno dello stesso conteggio di sessioni, a un flusso interessato. Per il volume totale abilitato per i sottotitoli, utilizzare [Conteggi sottotitoli](closed-captioning-count.md).

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag la prima volta che viene ricevuto un evento di avvio stato con didascalia durante la sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.states.closedcaptioning.set` quando [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | Voce [`mediaReporting.states[]`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/media-reporting-details) in cui `name = "closedCaptioning"`, campo `isSet` |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.set` |
