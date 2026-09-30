---
title: Errori
description: Segnala il numero di eventi di errore per sessione.
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
source-wordcount: '233'
ht-degree: 6%
---

# Errori

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la dimensione **Errori**. Adobe Analytics compila automaticamente una metrica di [eventi di errore](/help/reporting/metrics/error-events.md) associata dalla stessa variabile di dati di contesto `a.media.qoe.errorCount`. Customer Journey Analytics espone un singolo campo `xdm.mediaReporting.qoeDataDetails.errorCount` che è possibile utilizzare come dimensione o come metrica.*

>[!ENDSHADEBOX]

La dimensione **Errori** riporta il numero di eventi di errore ricevuti durante una sessione. Utilizza la dimensione per suddividere il coinvolgimento in base al conteggio esatto degli errori.

## Compilazione di questa dimensione

Il backend multimediale incrementa il conteggio in base a ogni errore segnalato dal lettore. Il valore viene segnalato nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.errorCount` quando [[!UICONTROL Media Quality]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `videoqoeerrorcountevar`, `post_videoqoeerrorcountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.errorCount` |

## Elementi dimensionali

Ogni elemento è il valore letterale del conteggio degli errori segnalato nella chiamata di chiusura. Per il reporting booleano a livello di sessione (se si è verificato un errore), utilizza [Flussi interessati dall&#39;errore](/help/reporting/metrics/error-impacted-streams.md). Per ID di errore univoci, utilizzare [ID di errore esterni](external-error-ids.md) e [ID di errore del lettore SDK](player-sdk-error-ids.md).

>[!NOTE]
>
>Se utilizzi il precedente SDK Heartbeat (Media SDK 1.5.x-2.x), gli ID di errore generati internamente da SDK vengono raccolti automaticamente nella chiave di dati contestuali `a.media.qoe.mediaSdkErrors` e accessibili in Adobe Analytics tramite una regola di elaborazione personalizzata. La caratteristica Audience Manager è `c_contextdata.a.media.qoe.mediaSdkErrors`. Questo campo non è applicabile alle implementazioni API Media Collection o Media Edge API.
