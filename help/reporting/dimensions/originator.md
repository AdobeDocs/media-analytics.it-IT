---
title: Iniziatore
description: Segnala l’autore o lo studio di produzione del contenuto.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 2%

---


# Iniziatore

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Originator**. Per informazioni su come raccogliere questa variabile, vedere [Iniziatore](/help/implementation/variables/standard-metadata/originator.md).*

>[!ENDSHADEBOX]

La dimensione **Iniziatore** segnala l&#39;autore o lo studio di produzione del contenuto (ad esempio, `"Warner Brothers"` o `"Sony"`). Utilizzalo per confrontare il coinvolgimento tra proprietari di contenuti o titolari di diritti.

## Compilazione di questa dimensione

L’iniziatore viene impostato dal lettore all’inizio della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics (regola di elaborazione) | Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.originator` a un eVar. |
| Adobe Analytics (classificazione) | Classificazione della dimensione [Contenuto (ID)](content.md): Adobe crea automaticamente questa classificazione quando **[[!UICONTROL Video Metadata]](/help/reporting/setup/analytics-reporting.md)** è abilitato per la suite di rapporti. È tua responsabilità popolare e mantenere i valori di classificazione. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.originator`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati (regola di elaborazione) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l&#39;eVar a cui la regola di elaborazione mappa `a.media.originator`) |
| Feed di dati (classificazione) | N/D: i feed di dati non supportano le classificazioni. |
| Audience Manager | `c_contextdata.a.media.originator` |

## Approccio di classificazione

Adobe crea automaticamente la struttura di classificazione del creatore quando **[[!UICONTROL Video Metadata]](/help/reporting/setup/analytics-reporting.md)** è abilitato per la suite di rapporti. Sei responsabile del popolamento e della gestione della classificazione utilizzando [Set di classificazione](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Questo approccio garantisce una relazione 1:1 tra ciascun ID contenuto e il suo creatore. Gli aggiornamenti delle classificazioni vengono applicati retroattivamente a tutti i dati storici per tale ID.

>[!IMPORTANT]
>
>Non modificare il nome della classificazione del creatore. Rinominandolo, Adobe può ricreare la classificazione originale, creando un duplicato.

## Approccio per le regole di elaborazione

Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.originator` a un eVar. Questo approccio acquisisce il creatore come valore per hit senza richiedere la manutenzione della classificazione.

Il compromesso è che si perde la relazione 1:1 garantita tra l&#39;iniziatore e la dimensione [Content (ID)](content.md) padre. Se l’implementazione invia valori non coerenti per lo stesso ID contenuto in più eventi, più originatori possono apparire sotto lo stesso contenuto. L’aggiornamento di un valore si applica solo ai dati a partire dal momento dell’aggiornamento.

## Elementi dimensionali

Ogni elemento è il valore letterale dell’iniziatore segnalato all’inizio della sessione. Utilizza un nome distinto e stabile per studio in modo che il coinvolgimento non si comprima tra entità non correlate.
