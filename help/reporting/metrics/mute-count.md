---
title: Conteggi disattivazione audio
description: Segnala quante volte il visualizzatore ha disattivato l'audio durante una sessione.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 9%

---


# Conteggi disattivazione audio

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica di reporting **Conteggi disattivazione audio**. Per informazioni su come raccogliere la variabile, vedere [Disattiva audio](/help/implementation/variables/player-state/mute.md).*

>[!ENDSHADEBOX]

La metrica **Conteggi disattivazione audio** indica quante volte il visualizzatore ha disattivato l&#39;audio durante una sessione. Ogni evento di disattivazione audio di avvio dello stato incrementa il conteggio. Accoppia con [Flussi interessati dalla disattivazione audio](mute-streams-impacted.md) per le aggregazioni booleane a livello di sessione e con [Durata totale disattivazione audio](mute-total-duration.md) per il tempo totale in stato.

## Come è calcolata questa metrica

Il backend multimediale incrementa questo conteggio su ogni evento di disattivazione audio stato-avvio. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.states.mute.count` quando [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | Voce [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) in cui `name = "mute"`, campo `count` |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.mute.count` |
