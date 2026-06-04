---
title: Errori
description: Segnala il numero di eventi di errore per sessione.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '231'
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
