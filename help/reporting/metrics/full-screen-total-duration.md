---
title: Durata totale schermo intero
description: Segnala i secondi cumulativi trascorsi dal visualizzatore a schermo intero durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 8%

---


# Durata totale schermo intero

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica di reporting **Durata totale schermo intero**. Per informazioni su come raccogliere questa variabile, consulta [Schermo intero](/help/implementation/variables/player-state/full-screen.md).*

>[!ENDSHADEBOX]

La metrica **Durata totale schermo intero** riporta il tempo cumulativo, in secondi, trascorso dal visualizzatore a schermo intero durante una sessione. Il backend somma ogni intervallo tra un evento di inizio stato a schermo intero e l’evento di fine stato corrispondente.

## Come è calcolata questa metrica

Il backend multimediale somma il tempo trascorso su tutti gli intervalli a schermo intero durante la sessione. La metrica viene segnalata nella chiamata di chiusura. Analysis Workspace mostra il valore come `HH:MM:SS`; Feed dati, Data Warehouse e API di reporting mostrano il valore in secondi.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.states.fullscreen.time` quando [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | Voce [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) in cui `name = "fullscreen"`, campo `time` |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.time` |
