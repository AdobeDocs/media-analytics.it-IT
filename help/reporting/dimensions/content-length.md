---
title: Durata del contenuto
description: Riporta la durata totale in secondi di ciascuna sessione multimediale come impostato all’inizio della sessione.
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
source-wordcount: '229'
ht-degree: 7%
---

# Durata del contenuto

>[!BEGINSHADEBOX]

*Questa pagina riguarda la dimensione di reporting **Lunghezza contenuto**. Per informazioni su come raccogliere questa variabile, vedere [Durata contenuto](/help/implementation/variables/core/content-length.md).*

>[!ENDSHADEBOX]

La dimensione **Lunghezza contenuto** riporta la durata totale in secondi di ogni sessione multimediale impostata all&#39;avvio della sessione. Attiva le metriche back-end, inclusi [indicatori di avanzamento](/help/reporting/metrics/progress-markers.md) e [Pubblico medio per minuto](/help/reporting/metrics/average-minute-audience.md).

## Compilazione di questa dimensione

La lunghezza del contenuto viene impostata dal lettore all’inizio della sessione. Il valore riportato è l’intera durata della risorsa in secondi, non la testina di riproduzione trascorsa.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.length` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `videolength`, `post_videolength` |
| Audience Manager | `c_contextdata.a.media.length` |

>[!NOTE]
>
>In Adobe Analytics, questo valore corrisponde anche a una classificazione **Video length** nella dimensione [Content](content.md). L’utente è responsabile di compilare e mantenere tale classificazione separatamente. Customer Journey Analytics utilizza direttamente questa dimensione. Se necessario, puoi utilizzare [Value bucketing](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/value-bucketing).

>[!IMPORTANT]
>
>Se la lunghezza del contenuto non è impostata o non è maggiore di zero, gli indicatori di avanzamento e il pubblico medio per minuto non vengono prodotti per quella sessione. Per i flussi live con durata sconosciuta, impostare `86400`.

## Elementi dimensionali

Ogni elemento rappresenta il valore di lunghezza letterale, in secondi, riportato all’inizio della sessione.
