---
title: Durata totale disattivazione audio
description: Segnala i secondi cumulativi in cui l’audio è stato disattivato durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 9%

---


# Durata totale disattivazione audio

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica di reporting **Durata totale disattivazione audio**. Per informazioni su come raccogliere la variabile, vedere [Disattiva audio](/help/implementation/variables/player-state/mute.md).*

>[!ENDSHADEBOX]

La metrica **Durata totale disattivazione audio** indica il tempo cumulativo in secondi in cui l&#39;audio è stato disattivato durante una sessione. Il backend somma ogni intervallo tra un evento di disattivazione audio e l’evento di fine stato corrispondente.

## Come è calcolata questa metrica

Il backend multimediale somma il tempo trascorso su tutti gli intervalli di disattivazione audio durante la sessione. La metrica viene segnalata nella chiamata di chiusura. Analysis Workspace mostra il valore come `HH:MM:SS`; Feed dati, Data Warehouse e API di reporting mostrano il valore in secondi.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.states.mute.time` quando [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | Voce [`mediaReporting.states[]`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/media-reporting-details) in cui `name = "mute"`, campo `time` |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.mute.time` |
