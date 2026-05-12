---
title: Nome del capitolo
description: Presenta il titolo del capitolo leggibile dall’utente.
feature: Dimensions
role: User, Admin
source-git-commit: 415d20722965d510458d3c09004b6991b05ac264
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 2%

---


# Nome del capitolo

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la dimensione di reporting **Nome capitolo**. Per informazioni su come raccogliere questa variabile, vedere [Nome capitolo](/help/implementation/variables/chapters/chapter-name.md).*

>[!ENDSHADEBOX]

La dimensione **Nome capitolo** fa emergere il titolo leggibile di ciascun capitolo (ad esempio, `"Pilot Episode - Opening"`).

## Compilazione di questa dimensione

Il nome del capitolo viene impostato dal lettore a ogni evento `media.chapterStart`.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics (regola di elaborazione) | Crea una [regola di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.chapter.friendlyName` a un eVar. |
| Adobe Analytics (classificazione) | Classificazione della dimensione [Chapter](chapter.md): Adobe crea automaticamente questa classificazione quando **[[!UICONTROL Media Chapters]](/help/reporting/media-reports-enable.md)** è abilitato per la suite di rapporti. È tua responsabilità popolare e mantenere i valori di classificazione. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feed di dati (regola di elaborazione) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l&#39;eVar a cui la regola di elaborazione mappa `a.media.chapter.friendlyName`) |
| Feed di dati (classificazione) | N/D: i feed di dati non supportano le classificazioni. |

## Approccio di classificazione

Adobe crea automaticamente la struttura di classificazione del nome del capitolo quando **[[!UICONTROL Media Chapters]](/help/reporting/media-reports-enable.md)** è abilitato per la suite di rapporti. Sei responsabile del popolamento e della gestione della classificazione utilizzando [Set di classificazione](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Questo approccio garantisce una relazione 1:1 tra ciascun ID capitolo e il relativo nome descrittivo. Gli aggiornamenti delle classificazioni vengono applicati retroattivamente a tutti i dati storici per tale ID.

>[!IMPORTANT]
>
>Non modificare il nome della classificazione del nome del capitolo. Rinominandolo, Adobe può ricreare la classificazione originale, creando un duplicato.

## Approccio per le regole di elaborazione

Crea una [regola di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.chapter.friendlyName` a un eVar. Questo approccio acquisisce il nome descrittivo come valore per hit senza richiedere la manutenzione della classificazione.

Il compromesso è che si perde la relazione 1:1 garantita tra il nome del capitolo e la dimensione [Chapter](chapter.md) padre. Se l’implementazione invia valori non coerenti per lo stesso ID capitolo tra gli eventi, è possibile che più nomi vengano visualizzati sotto lo stesso capitolo. L’aggiornamento di un valore si applica solo ai dati a partire dal momento dell’aggiornamento.

## Elementi dimensionali

Ogni elemento rappresenta il titolo letterale del capitolo riportato su `media.chapterStart`.
