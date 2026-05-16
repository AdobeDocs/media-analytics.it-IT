---
title: Conteggi schermo intero
description: Segnala quante volte il visualizzatore è entrato a schermo intero durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 8%

---


# Conteggi schermo intero

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica di reporting **Conteggi a schermo intero**. Per informazioni su come raccogliere questa variabile, consulta [Schermo intero](/help/implementation/variables/player-state/full-screen.md).*

>[!ENDSHADEBOX]

La metrica **Conteggi a schermo intero** indica quante volte il visualizzatore è entrato a schermo intero durante una sessione. Ogni evento di avvio a schermo intero incrementa il conteggio. Accoppia con [Flussi interessati dallo schermo intero](full-screen-streams-impacted.md) per aggregazioni booleane a livello di sessione e con [Durata totale schermo intero](full-screen-total-duration.md) per il tempo totale nello stato.

## Come è calcolata questa metrica

Il backend multimediale incrementa il campo `count` nella voce `fullscreen` di `mediaReporting.states[]` a ogni evento di avvio dello stato a schermo intero. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.states.fullscreen.count` quando [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | Voce [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) in cui `name = "fullscreen"`, campo `count` |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.count` |
