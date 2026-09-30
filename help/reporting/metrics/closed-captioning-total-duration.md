---
title: Durata totale sottotitoli
description: Segnala che i sottotitoli dei secondi cumulativi sono stati abilitati durante una sessione.
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
| Customer Journey Analytics | Voce [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) in cui `name = "closedCaptioning"`, campo `time` |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.time` |
