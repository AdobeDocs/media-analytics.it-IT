---
title: Flussi interessati da picture in picture
description: Conta le sessioni in cui il visualizzatore è entrato nell'immagine nell'immagine almeno una volta.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 7%

---


# Flussi interessati da picture in picture

>[!BEGINSHADEBOX]

*In questa pagina sono inclusi i **Flussi interessati dalla metrica di generazione rapporti immagine nell&#39;immagine**. Per informazioni su come raccogliere questa variabile, vedere [Immagine nell&#39;immagine](/help/implementation/variables/player-state/picture-in-picture.md).*

>[!ENDSHADEBOX]

La metrica **Flussi interessati da immagine nell&#39;immagine** conta le sessioni in cui il visualizzatore è entrato almeno una volta nella riproduzione immagine nell&#39;immagine. La metrica è un valore booleano a livello di sessione: più voci &quot;picture-in-picture&quot; all’interno dello stesso numero di sessioni corrispondono a un flusso interessato. Per il volume totale di ingresso immagine nell&#39;immagine, utilizzare [Conteggi immagine nell&#39;immagine](picture-in-picture-count.md).

## Come è calcolata questa metrica

Il backend multimediale imposta il flag `isSet` in `mediaReporting.states[]` per la voce `pictureInPicture` su `true` la prima volta che viene ricevuto un evento `media.statesUpdate` con `pictureInPicture` in `statesStart`. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.states.pictureinpicture.set` quando [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | Voce [`mediaReporting.states[]`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/media-reporting-details) in cui `name = "pictureInPicture"`, campo `isSet` |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.set` |
