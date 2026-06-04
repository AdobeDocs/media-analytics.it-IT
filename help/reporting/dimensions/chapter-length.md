---
title: Durata capitolo
description: Segnala la durata di ciascun capitolo.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 3%

---


# Durata capitolo

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Durata capitolo**. Per informazioni su come raccogliere questa variabile, vedere [Durata capitolo](/help/implementation/variables/chapters/chapter-length.md).*

>[!ENDSHADEBOX]

La dimensione **Durata capitolo** riporta la durata di ciascun capitolo, in secondi.

## Compilazione di questa dimensione

La lunghezza del capitolo viene impostata dal lettore a ogni evento [inizio capitolo](/help/implementation/events/chapters/chapter-start.md).

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics (regola di elaborazione) | Crea una [regola di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.chapter.length` a un eVar. |
| Adobe Analytics (classificazione) | Classificazione della dimensione [Chapter](chapter.md): Adobe crea automaticamente questa classificazione quando **[[!UICONTROL Media Chapters]](/help/reporting/setup/analytics-reporting.md)** è abilitato per la suite di rapporti. È tua responsabilità popolare e mantenere i valori di classificazione. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feed di dati (regola di elaborazione) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l&#39;eVar a cui la regola di elaborazione mappa `a.media.chapter.length`) |
| Feed di dati (classificazione) | N/D: i feed di dati non supportano le classificazioni. |
| Audience Manager | `c_contextdata.a.media.chapter.length` |

## Approccio di classificazione

Adobe crea automaticamente la struttura di classificazione della lunghezza del capitolo quando **[[!UICONTROL Media Chapters]](/help/reporting/setup/analytics-reporting.md)** è abilitato per la suite di rapporti. Sei responsabile del popolamento e della gestione della classificazione utilizzando [Set di classificazione](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Questo approccio garantisce una relazione 1:1 tra ciascun ID capitolo e la relativa lunghezza. Gli aggiornamenti delle classificazioni vengono applicati retroattivamente a tutti i dati storici per tale ID.

>[!IMPORTANT]
>
>Non modificare il nome della classificazione della lunghezza del capitolo. Rinominandolo, Adobe può ricreare la classificazione originale, creando un duplicato.

## Approccio per le regole di elaborazione

Crea una [regola di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.chapter.length` a un eVar. Questo approccio acquisisce la lunghezza del capitolo come valore per hit senza richiedere la manutenzione della classificazione.

Il compromesso è che si perde la relazione 1:1 garantita tra la lunghezza del capitolo e la dimensione [Chapter](chapter.md) padre. Se l’implementazione invia valori non coerenti per lo stesso ID capitolo in più eventi, è possibile che sotto lo stesso capitolo vengano visualizzate più lunghezze. L’aggiornamento di un valore si applica solo ai dati a partire dal momento dell’aggiornamento.

## Elementi dimensionali

Ogni elemento rappresenta il valore di lunghezza intero, in secondi, riportato all&#39;[inizio capitolo](/help/implementation/events/chapters/chapter-start.md).
