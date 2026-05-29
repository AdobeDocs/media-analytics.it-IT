---
title: ID creatività
description: Segnala l’identificatore creativo dell’annuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 3%

---


# ID creatività

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Creative ID**. Per informazioni su come raccogliere questa variabile, consulta [Creative ID](/help/implementation/variables/ads/creative-id.md).*

>[!ENDSHADEBOX]

La dimensione **Creative ID** riporta l&#39;identificatore creativo dell&#39;annuncio. Utilizza la dimensione per aggregare il coinvolgimento tra gli annunci che condividono un contenuto creativo.

## Compilazione di questa dimensione

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics (regola di elaborazione) | Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.ad.creative` a un eVar. |
| Adobe Analytics (classificazione) | Classificazione della dimensione [Ad](ad.md): Adobe crea automaticamente questa classificazione quando **[[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md)** è abilitato per la suite di rapporti. È tua responsabilità popolare e mantenere i valori di classificazione. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.creativeID`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feed di dati (regola di elaborazione) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l&#39;eVar a cui la regola di elaborazione mappa `a.media.ad.creative`) |
| Feed di dati (classificazione) | N/D: i feed di dati non supportano le classificazioni. |
| Audience Manager | `c_contextdata.a.media.ad.creative` |

## Approccio di classificazione

Adobe crea automaticamente la struttura di classificazione Creative ID quando **[[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md)** è abilitato per la suite di rapporti. Sei responsabile del popolamento e della gestione della classificazione utilizzando [Set di classificazione](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Questo approccio garantisce una relazione 1:1 tra ciascun ID annuncio e il relativo ID creativo. Gli aggiornamenti delle classificazioni vengono applicati retroattivamente a tutti i dati storici per tale ID.

>[!IMPORTANT]
>
>Non modificare il nome della classificazione Creative ID. Rinominandolo, Adobe può ricreare la classificazione originale, creando un duplicato.

## Approccio per le regole di elaborazione

Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.ad.creative` a un eVar. Questo approccio acquisisce l’ID creativo come valore per hit senza richiedere la manutenzione della classificazione.

Il compromesso è che si perde la relazione 1:1 garantita tra l&#39;ID creativo e la dimensione [Ad](ad.md) padre. Se l’implementazione invia valori non coerenti per lo stesso ID annuncio in più eventi, è possibile che più ID creativi vengano visualizzati sotto lo stesso annuncio. L’aggiornamento di un valore si applica solo ai dati a partire dal momento dell’aggiornamento.

## Elementi dimensionali

Ogni elemento è un ID creativo univoco. Utilizza un identificatore stabile per creatività in modo che la stessa creatività possa essere aggregata a un singolo elemento nelle campagne.
