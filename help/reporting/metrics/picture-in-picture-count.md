---
title: Conteggio immagini nell’immagine (Picture in Picture)
description: Segnala quante volte il visualizzatore è entrato "picture-in-picture" durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 8%

---


# Conteggio immagini nell’immagine (Picture in Picture)

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica di reporting **Conteggi immagine nell&#39;immagine**. Per informazioni su come raccogliere questa variabile, vedere [Immagine nell&#39;immagine](/help/implementation/variables/player-state/picture-in-picture.md).*

>[!ENDSHADEBOX]

La metrica **Conteggi immagine nell&#39;immagine** indica quante volte il visualizzatore è entrato in riproduzione immagine nell&#39;immagine durante una sessione. Ogni evento di avvio dello stato immagine nell&#39;immagine incrementa il conteggio. Coppia con [Flussi interessati dall&#39;immagine nell&#39;immagine](picture-in-picture-streams-impacted.md) per le aggregazioni booleane a livello di sessione e con [Durata totale immagine nell&#39;immagine](picture-in-picture-total-duration.md) per il tempo totale nello stato.

## Come è calcolata questa metrica

Il backend multimediale incrementa questo conteggio su ogni evento di avvio dello stato immagine nell’immagine. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.states.pictureinpicture.count` quando [[!UICONTROL Player State Tracking]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | Voce [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) in cui `name = "pictureInPicture"`, campo `count` |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.count` |
