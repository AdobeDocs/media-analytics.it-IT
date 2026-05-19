---
title: Durata totale immagine nell’immagine (Picture in Picture)
description: Segnala i secondi cumulativi trascorsi dal visualizzatore nell’immagine nell’immagine durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 8%

---


# Durata totale immagine nell’immagine (Picture in Picture)

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica di reporting **Durata totale immagine nell&#39;immagine**. Per informazioni su come raccogliere questa variabile, vedere [Immagine nell&#39;immagine](/help/implementation/variables/player-state/picture-in-picture.md).*

>[!ENDSHADEBOX]

La metrica **Durata totale immagine nell&#39;immagine** riporta il tempo cumulativo, in secondi, trascorso dal visualizzatore nell&#39;immagine nell&#39;immagine durante una sessione. Il backend somma ogni intervallo tra un evento di inizio stato immagine nell’immagine e l’evento di fine stato corrispondente.

## Come è calcolata questa metrica

Il backend multimediale somma il tempo trascorso su tutti gli intervalli immagine nell’immagine durante la sessione. La metrica viene segnalata nella chiamata di chiusura. Analysis Workspace mostra il valore come `HH:MM:SS`; Feed dati, Data Warehouse e API di reporting mostrano il valore in secondi.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.states.pictureinpicture.time` quando [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | Voce [`mediaReporting.states[]`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/media-reporting-details) in cui `name = "pictureInPicture"`, campo `time` |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.time` |
