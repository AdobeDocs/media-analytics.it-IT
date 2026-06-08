---
title: Posizione del pod
description: Segnala l’offset di ogni interruzione pubblicitaria all’interno del contenuto.
feature: Dimensions
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 2%

---


# Posizione del pod

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Posizione pod**. Per informazioni su come raccogliere questa variabile, vedere [Ora di inizio dell&#39;interruzione pubblicitaria](/help/implementation/variables/ads/ad-break-start-time.md).*

>[!ENDSHADEBOX]

La dimensione **Posizione pod** riporta l&#39;offset di ogni interruzione pubblicitaria all&#39;interno del contenuto, in secondi. Un pre-roll ha posizione `0`; i mid-roll hanno posizioni corrispondenti all&#39;ora di inizio della testina di riproduzione.

## Compilazione di questa dimensione

La posizione del pod è impostata dal valore [Ora di inizio interruzione annuncio](/help/implementation/variables/ads/ad-break-start-time.md) impostato dal lettore all&#39;[inizio interruzione annuncio](/help/implementation/events/ads/ad-break-start.md).

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics (regola di elaborazione) | Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.ad.podSecond` a un eVar. |
| Adobe Analytics (classificazione) | Classificazione della dimensione [Ad pod](ad-pod.md). Adobe crea automaticamente questa classificazione quando **[[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md)** è abilitato per la suite di rapporti. È tua responsabilità popolare e mantenere i valori di classificazione. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.offset`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Feed di dati (regola di elaborazione) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l&#39;eVar a cui la regola di elaborazione mappa `a.media.ad.podSecond`) |
| Feed di dati (classificazione) | N/D: i feed di dati non supportano le classificazioni. |
| Audience Manager | `c_contextdata.a.media.ad.podSecond` |

## Approccio di classificazione

Adobe crea automaticamente la struttura di classificazione della posizione del pod quando **[[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md)** è abilitato per la suite di rapporti. Sei responsabile del popolamento e della gestione della classificazione utilizzando [Set di classificazione](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Questo approccio garantisce una relazione 1:1 tra ciascun ID ad pod e la relativa posizione. Gli aggiornamenti delle classificazioni vengono applicati retroattivamente a tutti i dati storici per tale ID.

>[!IMPORTANT]
>
>Non modificare il nome della classificazione della posizione del pod. Rinominandolo, Adobe può ricreare la classificazione originale, creando un duplicato.

## Approccio per le regole di elaborazione

Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.ad.podSecond` a un eVar. Questo approccio acquisisce la posizione del pod come valore per hit senza richiedere la manutenzione della classificazione.

Il compromesso è che si perde la relazione 1:1 garantita tra la posizione del pod e la dimensione [Ad pod](ad-pod.md) padre. Se l’implementazione invia valori non coerenti per lo stesso ID pod in più eventi, è possibile che più posizioni vengano visualizzate sotto lo stesso pod annuncio. L’aggiornamento di un valore si applica solo ai dati a partire dal momento dell’aggiornamento.

## Elementi dimensionali

Ogni elemento è il valore di offset intero (in secondi) riportato all&#39;avvio dell&#39;[interruzione annuncio](/help/implementation/events/ads/ad-break-start.md).
