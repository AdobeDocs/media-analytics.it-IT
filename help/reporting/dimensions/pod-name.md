---
title: Nome del pod
description: Segnala il nome descrittivo di ogni interruzione pubblicitaria. Raccolgilo in Adobe Analytics utilizzando una classificazione o una regola di elaborazione personalizzata.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 1%

---


# Nome del pod

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Nome pod**. Per informazioni su come raccogliere questa variabile, vedere [Nome interruzione annuncio](/help/implementation/variables/ads/ad-break-name.md).*

>[!ENDSHADEBOX]

La dimensione **Pod name** riporta il nome descrittivo di ogni interruzione pubblicitaria (ad esempio, `"pre-roll"`, `"mid-roll-1"`). In Customer Journey Analytics è una dimensione discreta compilata direttamente dalla variabile di implementazione. In Adobe Analytics è disponibile tramite due approcci: una classificazione della dimensione [Ad pod](ad-pod.md) o un eVar popolato utilizzando una regola di elaborazione.

## Compilazione di questa dimensione

Il nome del pod proviene dal valore [Nome interruzione annuncio](/help/implementation/variables/ads/ad-break-name.md) impostato dal lettore all&#39;[inizio interruzione annuncio](/help/implementation/events/ads/ad-break-start.md).

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics (regola di elaborazione) | Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.ad.podFriendlyName` a un eVar. |
| Adobe Analytics (classificazione) | Classificazione della dimensione del pod dell&#39;annuncio: Adobe crea automaticamente questa classificazione quando **[[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md)** è abilitato per la suite di rapporti. È tua responsabilità popolare e mantenere i valori di classificazione. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Feed di dati (regola di elaborazione) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l&#39;eVar a cui la regola di elaborazione mappa `a.media.ad.podFriendlyName`) |
| Feed di dati (classificazione) | N/D: i feed di dati non supportano le classificazioni. |
| Audience Manager | `c_contextdata.a.media.ad.podFriendlyName` |

## Approccio di classificazione

Adobe crea automaticamente la struttura di classificazione del nome del pod quando **[[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md)** è abilitato per la suite di rapporti. Sei responsabile del popolamento e della gestione della classificazione utilizzando [Set di classificazione](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Questo approccio garantisce una relazione 1:1 tra ciascun ID pod e il relativo nome descrittivo. Gli aggiornamenti delle classificazioni vengono applicati retroattivamente a tutti i dati storici per tale ID.

>[!IMPORTANT]
>
>Non modificare il nome della classificazione del nome del pod. Rinominandolo, Adobe può ricreare la classificazione originale, creando un duplicato.

## Approccio per le regole di elaborazione

Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.ad.podFriendlyName` a un eVar. Questo approccio acquisisce il nome descrittivo come valore per hit senza richiedere la manutenzione della classificazione.

Il compromesso è che si perde la relazione 1:1 garantita tra il nome del pod e la dimensione [Ad pod](ad-pod.md) padre. Se l’implementazione invia valori non coerenti per lo stesso ID pod in più eventi, è possibile che più nomi vengano visualizzati sotto lo stesso pod annuncio. L’aggiornamento di un valore si applica solo ai dati a partire dal momento dell’aggiornamento.

## Elementi dimensionali

Ogni elemento rappresenta il nome letterale dell&#39;interruzione pubblicitaria segnalato all&#39;[inizio interruzione pubblicitaria](/help/implementation/events/ads/ad-break-start.md).
