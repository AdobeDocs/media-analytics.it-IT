---
title: Conteggi schermo intero
description: Segnala quante volte il visualizzatore è entrato a schermo intero durante una sessione.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 9%
---

# Conteggi schermo intero

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica di reporting **Conteggi a schermo intero**. Per informazioni su come raccogliere questa variabile, consulta [Schermo intero](/help/implementation/variables/player-state/full-screen.md).*

>[!ENDSHADEBOX]

La metrica **Conteggi a schermo intero** indica quante volte il visualizzatore è entrato a schermo intero durante una sessione. Ogni evento di avvio a schermo intero incrementa il conteggio. Accoppia con [Flussi interessati dallo schermo intero](full-screen-streams-impacted.md) per aggregazioni booleane a livello di sessione e con [Durata totale schermo intero](full-screen-total-duration.md) per il tempo totale nello stato.

## Come è calcolata questa metrica

Il backend multimediale incrementa questo conteggio su ogni evento di avvio dello stato a schermo intero. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.states.fullscreen.count` quando [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | Voce [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) in cui `name = "fullscreen"`, campo `count` |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.count` |
