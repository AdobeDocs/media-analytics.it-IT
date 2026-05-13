---
title: Conteggi dei sottotitoli
description: Segnala quante volte il visualizzatore ha abilitato i sottotitoli durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 7%

---


# Conteggi dei sottotitoli

>[!BEGINSHADEBOX]

*In questa pagina sono incluse le **metriche di reporting dei conteggi dei sottotitoli**. Vedi [Sottotitoli](/help/implementation/variables/player-state/closed-captioning.md) per informazioni su come raccogliere questa variabile.*

>[!ENDSHADEBOX]

La metrica **Conteggi sottotitoli** indica quante volte il visualizzatore ha abilitato i sottotitoli durante una sessione. Ogni evento di avvio dello stato abilitato alla didascalia incrementa il conteggio. Coppia con [Flussi interessati dai sottotitoli](closed-captioning-streams-impacted.md) per le aggregazioni booleane a livello di sessione e con [Durata totale dei sottotitoli](closed-captioning-total-duration.md) per il tempo totale nello stato.

## Come è calcolata questa metrica

Il backend multimediale incrementa il campo `count` nella voce `closedCaptioning` di `mediaReporting.states[]` a ogni evento di avvio dello stato di attivazione didascalia. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.states.closedcaptioning.count` quando [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | Voce [`mediaReporting.states[]`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/media-reporting-details) in cui `name = "closedCaptioning"`, campo `count` |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
