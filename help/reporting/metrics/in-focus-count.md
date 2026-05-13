---
title: Conteggi in focus
description: Segnala quante volte il lettore ha ottenuto lo stato attivo durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 7%

---


# Conteggi in focus

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica di reporting **In focus count**. Per informazioni su come raccogliere questa variabile, vedere [In focus](/help/implementation/variables/player-state/in-focus.md).*

>[!ENDSHADEBOX]

La metrica **In focus count** riporta il numero di volte in cui il lettore ha acquisito lo stato attivo durante una sessione. Ogni evento di inizio stato focus incrementa il conteggio. Accoppia con [Flussi interessati da in focus](in-focus-streams-impacted.md) per aggregazioni booleane a livello di sessione e con [Durata totale in focus](in-focus-total-duration.md) per il tempo totale in stato.

## Come è calcolata questa metrica

Il backend multimediale incrementa il campo `count` nella voce `inFocus` di `mediaReporting.states[]` a ogni evento di avvio dello stato attivo. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.states.infocus.count` quando [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | Voce [`mediaReporting.states[]`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/media-reporting-details) in cui `name = "inFocus"`, campo `count` |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
