---
title: Flussi interessati dalla disattivazione audio
description: Conta le sessioni in cui il visualizzatore ha disattivato l'audio almeno una volta.
feature: Metrics
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 9%

---


# Flussi interessati dalla disattivazione audio

>[!BEGINSHADEBOX]

*In questa pagina sono inclusi i **Flussi interessati dalla metrica di reporting Disattiva audio**. Per informazioni su come raccogliere la variabile, vedere [Disattiva audio](/help/implementation/variables/player-state/mute.md).*

>[!ENDSHADEBOX]

La metrica **Flussi interessati dalla disattivazione audio** conta le sessioni in cui il visualizzatore ha disattivato l&#39;audio almeno una volta. La metrica è un valore booleano a livello di sessione; più disattivazioni audio all’interno dello stesso conteggio di sessioni di un flusso interessato. Per il volume totale disattivato, utilizzare [Conteggi disattivati](mute-count.md).

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag la prima volta che viene ricevuto un evento di disattivazione audio stato-inizio durante la sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.states.mute.set` quando [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | Voce [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/media-reporting-details) in cui `name = "mute"`, campo `isSet` |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.mute.set` |
