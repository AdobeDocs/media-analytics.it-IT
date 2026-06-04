---
title: Durata totale sottotitoli
description: Segnala che i sottotitoli dei secondi cumulativi sono stati abilitati durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 8%

---


# Durata totale sottotitoli

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica di reporting **Durata totale sottotitoli**. Vedi [Sottotitoli](/help/implementation/variables/player-state/closed-captioning.md) per informazioni su come raccogliere questa variabile.*

>[!ENDSHADEBOX]

La metrica **Durata totale sottotitoli** riporta il tempo cumulativo, in secondi, in cui i sottotitoli sono stati abilitati durante una sessione. Il backend somma ogni intervallo tra un evento di inizio stato con didascalia e l’evento di fine stato corrispondente.

## Come è calcolata questa metrica

Il backend dei contenuti multimediali somma il tempo trascorso su tutti gli intervalli abilitati per i sottotitoli durante la sessione. La metrica viene segnalata nella chiamata di chiusura. Analysis Workspace mostra il valore come `HH:MM:SS`; Feed dati, Data Warehouse e API di reporting mostrano il valore in secondi.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.states.closedcaptioning.time` quando [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | Voce [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/media-reporting-details) in cui `name = "closedCaptioning"`, campo `time` |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.time` |
