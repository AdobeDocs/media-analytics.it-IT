---
title: Durata totale in focus
description: Segnala i secondi cumulativi in cui il lettore era attivo durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 8%

---


# Durata totale in focus

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica di reporting **Durata totale in focus**. Per informazioni su come raccogliere questa variabile, vedere [In focus](/help/implementation/variables/player-state/in-focus.md).*

>[!ENDSHADEBOX]

La metrica **Durata totale in focus** riporta il tempo cumulativo, in secondi, in cui il lettore è rimasto attivo durante una sessione. Il backend somma ogni intervallo tra un evento di inizio stato attivazione e l’evento di fine stato corrispondente.

## Come è calcolata questa metrica

Il backend multimediale somma il tempo trascorso su tutti gli intervalli in focus durante la sessione. La metrica viene segnalata nella chiamata di chiusura. Analysis Workspace mostra il valore come `HH:MM:SS`; Feed dati, Data Warehouse e API di reporting mostrano il valore in secondi.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.states.infocus.time` quando [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | Voce [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) in cui `name = "inFocus"`, campo `time` |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.infocus.time` |
