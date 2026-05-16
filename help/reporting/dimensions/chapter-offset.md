---
title: Offset capitolo
description: Segnala l’offset di ciascun capitolo all’interno del contenuto.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 2%

---


# Offset capitolo

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Offset capitolo**. Per informazioni su come raccogliere questa variabile, vedere [Offset capitolo](/help/implementation/variables/chapters/chapter-offset.md).*

>[!ENDSHADEBOX]

La dimensione **Offset capitolo** riporta lo scostamento di ciascun capitolo all&#39;interno del contenuto, misurato in secondi dall&#39;inizio.

## Compilazione di questa dimensione

L&#39;offset del capitolo viene impostato dal lettore a ogni evento [chapter start](/help/implementation/events/chapters/chapter-start.md).

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics (regola di elaborazione) | Crea una [regola di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.chapter.offset` a un eVar. |
| Adobe Analytics (classificazione) | Classificazione della dimensione [Chapter](chapter.md): Adobe crea automaticamente questa classificazione quando **[[!UICONTROL Media Chapters]](/help/reporting/media-reports-enable.md)** è abilitato per la suite di rapporti. È tua responsabilità popolare e mantenere i valori di classificazione. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feed di dati (regola di elaborazione) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l&#39;eVar a cui la regola di elaborazione mappa `a.media.chapter.offset`) |
| Feed di dati (classificazione) | N/D: i feed di dati non supportano le classificazioni. |
| Audience Manager | `c_contextdata.a.media.chapter.offset` |

## Approccio di classificazione

Adobe crea automaticamente la struttura di classificazione di offset del capitolo quando **[[!UICONTROL Media Chapters]](/help/reporting/media-reports-enable.md)** è abilitato per la suite di rapporti. Sei responsabile del popolamento e della gestione della classificazione utilizzando [Set di classificazione](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Questo approccio garantisce una relazione 1:1 tra ciascun ID capitolo e il relativo offset. Gli aggiornamenti delle classificazioni vengono applicati retroattivamente a tutti i dati storici per tale ID.

>[!IMPORTANT]
>
>Non modificare il nome della classificazione di offset del capitolo. Rinominandolo, Adobe può ricreare la classificazione originale, creando un duplicato.

## Approccio per le regole di elaborazione

Crea una [regola di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.chapter.offset` a un eVar. Questo approccio acquisisce l’offset del capitolo come valore per hit senza richiedere la manutenzione della classificazione.

Il compromesso è che si perde la relazione 1:1 garantita tra l&#39;offset del capitolo e la dimensione [Chapter](chapter.md) padre. Se l’implementazione invia valori non coerenti per lo stesso ID capitolo tra gli eventi, è possibile che più offset vengano visualizzati sotto lo stesso capitolo. L’aggiornamento di un valore si applica solo ai dati a partire dal momento dell’aggiornamento.

## Elementi dimensionali

Ogni elemento rappresenta il valore di offset intero espresso in secondi riportato all&#39;[inizio capitolo](/help/implementation/events/chapters/chapter-start.md).
