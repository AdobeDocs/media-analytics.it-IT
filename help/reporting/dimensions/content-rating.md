---
title: Valutazione dei contenuti
description: Riporta la valutazione del pubblico come definito dalle Linee guida TV per genitori o da un sistema di valutazione regionale.
feature: Dimensions
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 2%

---


# Valutazione dei contenuti

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Valutazione contenuto**. Per informazioni su come raccogliere questa variabile, vedere [Valutazione contenuto](/help/implementation/variables/standard-metadata/content-rating.md).*

>[!ENDSHADEBOX]

La dimensione **Valutazione contenuto** riporta la valutazione del pubblico per ogni sessione. Utilizzalo per confrontare il coinvolgimento e il carico di annunci tra i livelli di valutazione.

## Compilazione di questa dimensione

La classificazione del contenuto viene impostata dal lettore all’inizio della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics (regola di elaborazione) | Crea una [regola di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.rating` a un eVar. |
| Adobe Analytics (classificazione) | Classificazione della dimensione [Contenuto (ID)](content.md). Adobe crea automaticamente questa classificazione quando **[[!UICONTROL Video Metadata]](/help/reporting/setup/analytics-reporting.md)** è abilitato per la suite di rapporti. È tua responsabilità popolare e mantenere i valori di classificazione. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.rating`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati (regola di elaborazione) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l&#39;eVar a cui la regola di elaborazione mappa `a.media.rating`) |
| Feed di dati (classificazione) | N/D: i feed di dati non supportano le classificazioni. |
| Audience Manager | `c_contextdata.a.media.rating` |

## Approccio di classificazione

Adobe crea automaticamente la struttura di classificazione della classificazione della classificazione dei contenuti quando **[[!UICONTROL Video Metadata]](/help/reporting/setup/analytics-reporting.md)** è abilitato per la suite di rapporti. Sei responsabile del popolamento e della gestione della classificazione utilizzando [Set di classificazione](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Questo approccio garantisce una relazione 1:1 tra ciascun ID contenuto e la relativa valutazione. Gli aggiornamenti delle classificazioni vengono applicati retroattivamente a tutti i dati storici per tale ID.

>[!IMPORTANT]
>
>Non modificare il nome della classificazione di classificazione della classificazione dei contenuti. Rinominandolo, Adobe può ricreare la classificazione originale, creando un duplicato.

## Approccio per le regole di elaborazione

Crea una [regola di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.rating` a un eVar. Questo approccio acquisisce la valutazione del contenuto come valore per hit senza richiedere la manutenzione della classificazione.

Il compromesso è che si perde la relazione 1:1 garantita tra la valutazione del contenuto e la dimensione [Contenuto (ID)](content.md) padre. Se l’implementazione invia valori non coerenti per lo stesso ID contenuto tra gli eventi, è possibile che più valutazioni vengano visualizzate sotto lo stesso contenuto. L’aggiornamento di un valore si applica solo ai dati a partire dal momento dell’aggiornamento.

## Elementi dimensionali

Ogni elemento rappresenta il valore di valutazione letterale riportato all&#39;inizio della sessione (ad esempio, `"TVY"`, `"TVG"`, `"TVPG"`, `"TVMA"`). Attieniti a un insieme fisso di valori per sistema di valutazione per evitare la frammentazione delle voci.
