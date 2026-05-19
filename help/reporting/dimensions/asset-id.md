---
title: ID risorsa
description: Segnala un identificatore di settore stabile per la risorsa multimediale sottostante.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 2%

---


# ID risorsa

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **ID risorsa**. Per informazioni su come raccogliere questa variabile, consulta [ID risorsa](/help/implementation/variables/standard-metadata/asset-id.md).*

>[!ENDSHADEBOX]

La dimensione **ID risorsa** riporta un identificatore stabile del settore per la risorsa multimediale sottostante (in genere un EIDR, TMS/Gracenote o un ID Rovi, ma sono accettati anche ID proprietari).

## Compilazione di questa dimensione

L’ID risorsa viene impostato dal lettore all’inizio della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics (regola di elaborazione) | Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.asset` a un eVar. |
| Adobe Analytics (classificazione) | Classificazione della dimensione [Contenuto (ID)](content.md): Adobe crea automaticamente questa classificazione quando **[[!UICONTROL Video Metadata]](/help/reporting/media-reports-enable.md)** è abilitato per la suite di rapporti. È tua responsabilità popolare e mantenere i valori di classificazione. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.assetID`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati (regola di elaborazione) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l&#39;eVar a cui la regola di elaborazione mappa `a.media.asset`) |
| Feed di dati (classificazione) | N/D: i feed di dati non supportano le classificazioni. |
| Audience Manager | `c_contextdata.a.media.asset` |

## Approccio di classificazione

Adobe crea automaticamente la struttura di classificazione Asset ID quando **[[!UICONTROL Video Metadata]](/help/reporting/media-reports-enable.md)** è abilitato per la suite di rapporti. Sei responsabile del popolamento e della gestione della classificazione utilizzando [Set di classificazione](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Questo approccio garantisce una relazione 1:1 tra ciascun ID contenuto e il relativo ID risorsa. Gli aggiornamenti delle classificazioni vengono applicati retroattivamente a tutti i dati storici per tale ID.

>[!IMPORTANT]
>
>Non modificare il nome della classificazione ID risorsa. Rinominandolo, Adobe può ricreare la classificazione originale, creando un duplicato.

## Approccio per le regole di elaborazione

Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.asset` a un eVar. Questo approccio acquisisce l’ID risorsa come valore per hit senza richiedere la manutenzione della classificazione.

Il compromesso è che si perde la relazione 1:1 garantita tra l&#39;ID risorsa e la dimensione [Contenuto (ID)](content.md) padre. Se l’implementazione invia valori non coerenti per lo stesso ID contenuto in più eventi, è possibile che più ID risorsa vengano visualizzati sotto lo stesso contenuto. L’aggiornamento di un valore si applica solo ai dati a partire dal momento dell’aggiornamento.

## Elementi dimensionali

Ciascuna voce rappresenta un valore ID univoco del cespite segnalato durante il periodo di riferimento. Utilizza un singolo identificatore stabile per risorsa in tutte le piattaforme di distribuzione, in modo che lo stesso contenuto possa essere aggregato a un singolo elemento.
