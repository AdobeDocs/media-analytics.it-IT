---
title: Data prima versione digitale
description: Segnala la data in cui il contenuto è apparso per la prima volta su una piattaforma digitale.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 3%
---

# Data prima versione digitale

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **First digital date**. Per informazioni su come raccogliere questa variabile, vedere [Prima data digitale](/help/implementation/variables/standard-metadata/first-digital-date.md).*

>[!ENDSHADEBOX]

La dimensione **Prima data digitale** riporta la data in cui il contenuto è apparso per la prima volta su una piattaforma digitale. Utilizzala insieme alla [Data della prima messa in onda](first-air-date.md) per confrontare gli intervalli di rilascio digitali con quelli della trasmissione originale.

## Compilazione di questa dimensione

La prima data digitale viene impostata dal lettore all’inizio della sessione.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics (regola di elaborazione) | Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.digitalDate` a un eVar. |
| Adobe Analytics (classificazione) | Classificazione della dimensione [Contenuto (ID)](content.md). Adobe crea automaticamente questa classificazione quando **[[!UICONTROL Video Metadata]](/help/reporting/setup/analytics-reporting.md)** è abilitato per la suite di rapporti. È tua responsabilità popolare e mantenere i valori di classificazione. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.firstDigitalDate`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati (regola di elaborazione) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l&#39;eVar a cui la regola di elaborazione mappa `a.media.digitalDate`) |
| Feed di dati (classificazione) | N/D: i feed di dati non supportano le classificazioni. |
| Audience Manager | `c_contextdata.a.media.digitalDate` |

## Approccio di classificazione

Adobe crea automaticamente la struttura di classificazione della prima data digitale quando **[[!UICONTROL Video Metadata]](/help/reporting/setup/analytics-reporting.md)** è abilitato per la suite di rapporti. Sei responsabile del popolamento e della gestione della classificazione utilizzando [Set di classificazione](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Questo approccio garantisce una relazione 1:1 tra ciascun ID contenuto e la sua prima data digitale. Gli aggiornamenti delle classificazioni vengono applicati retroattivamente a tutti i dati storici per tale ID.

>[!IMPORTANT]
>
>Non modificare il nome di classificazione della prima data digitale. Rinominandolo, Adobe può ricreare la classificazione originale, creando un duplicato.

## Approccio per le regole di elaborazione

Crea una [regola di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) che associa `a.media.digitalDate` a un eVar. Questo approccio acquisisce la prima data digitale come valore per hit senza richiedere la manutenzione della classificazione.

Il compromesso è che si perde la relazione 1:1 garantita tra la prima data digitale e la dimensione [Contenuto (ID)](content.md) padre. Se l’implementazione invia valori non coerenti per lo stesso ID contenuto in più eventi, è possibile che più date digitali vengano visualizzate sotto lo stesso contenuto. L’aggiornamento di un valore si applica solo ai dati a partire dal momento dell’aggiornamento.

## Elementi dimensionali

Ogni elemento rappresenta la stringa di data letterale riportata all’inizio della sessione. Utilizza un formato coerente nelle diverse implementazioni. Adobe consiglia `YYYY-MM-DD`.
