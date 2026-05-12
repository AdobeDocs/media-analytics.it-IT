---
title: Data della prima messa in onda
description: Riporta la data in cui il contenuto è andato in onda per la prima volta in televisione.
feature: Dimensions
role: User, Admin
source-git-commit: 415d20722965d510458d3c09004b6991b05ac264
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 3%

---


# Data della prima messa in onda

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la dimensione di reporting **Data prima messa in onda**. Per informazioni su come raccogliere questa variabile, consulta [Prima data di trasmissione](/help/implementation/variables/standard-metadata/first-air-date.md).*

>[!ENDSHADEBOX]

La dimensione **Data prima messa in onda** riporta la data in cui il contenuto è andato in onda per la prima volta in televisione. Utilizzala per separare il coinvolgimento sulle nuove versioni dal coinvolgimento su contenuti meno recenti.

## Compilazione di questa dimensione

La data della prima messa in onda viene impostata dal lettore all’inizio della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics (regola di elaborazione) | Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.airDate` a un eVar. |
| Adobe Analytics (classificazione) | Classificazione della dimensione [Contenuto (ID)](content.md): Adobe crea automaticamente questa classificazione quando **[[!UICONTROL Video Metadata]](/help/reporting/media-reports-enable.md)** è abilitato per la suite di rapporti. È tua responsabilità popolare e mantenere i valori di classificazione. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.firstAirDate`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati (regola di elaborazione) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l&#39;eVar a cui la regola di elaborazione mappa `a.media.airDate`) |
| Feed di dati (classificazione) | N/D: i feed di dati non supportano le classificazioni. |

## Approccio di classificazione

Adobe crea automaticamente la struttura di classificazione della prima data di trasmissione quando **[[!UICONTROL Video Metadata]](/help/reporting/media-reports-enable.md)** è abilitato per la suite di rapporti. Sei responsabile del popolamento e della gestione della classificazione utilizzando [Set di classificazione](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Questo approccio garantisce una relazione 1:1 tra ciascun ID contenuto e la sua prima data di messa in onda. Gli aggiornamenti delle classificazioni vengono applicati retroattivamente a tutti i dati storici per tale ID.

>[!IMPORTANT]
>
>Non modificare il nome di classificazione della data di prima messa in onda. Rinominandolo, Adobe può ricreare la classificazione originale, creando un duplicato.

## Approccio per le regole di elaborazione

Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.airDate` a un eVar. Questo approccio acquisisce la prima data di messa in onda come valore per hit senza richiedere la manutenzione della classificazione.

Il compromesso è che si perde la relazione 1:1 garantita tra la data della prima messa in onda e la dimensione [Content (ID)](content.md) padre. Se l’implementazione invia valori non coerenti per lo stesso ID contenuto in tutti gli eventi, è possibile che più date di prima messa in onda vengano visualizzate sotto lo stesso contenuto. L’aggiornamento di un valore si applica solo ai dati a partire dal momento dell’aggiornamento.

## Elementi dimensionali

Ogni elemento rappresenta la stringa di data letterale riportata all’inizio della sessione. Utilizza un formato coerente nelle diverse implementazioni. Adobe consiglia `YYYY-MM-DD`.
