---
title: Indicatori di avanzamento
description: Conta le sessioni la cui testina di riproduzione ha superato ciascuna delle cinque soglie fisse (10%, 25%, 50%, 75% e 95%).
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 8%

---


# Indicatori di avanzamento

Gli **Indicatori di avanzamento** sono cinque metriche separate che contano le sessioni la cui testina di riproduzione ha superato ciascuna di cinque soglie fisse (10%, 25%, 50%, 75% e 95% della lunghezza del contenuto). Utilizzali per tracciare l&#39;elenco a discesa in tutto il runtime di contenuto; abbina con [Inizio contenuto](content-starts.md) per calcolare la condivisione delle sessioni avviate che hanno raggiunto ogni fase cardine.

Ogni marcatore viene attivato una volta per sessione e non viene riattivato durante la ricerca. I marcatori saltati quando si cerca in avanti non vengono conteggiati (ad esempio, un visualizzatore che passa dal 5% al 60% attiva i marcatori del 10%, 25% e 50% tutti contemporaneamente).

## Come viene calcolato ciascun marcatore

Il backend multimediale valuta la testina di riproduzione riportata rispetto a `Content length` dopo ogni evento. Quando l&#39;indicatore di riproduzione supera per la prima volta una soglia, il valore booleano `mediaReporting.sessionDetails.hasProgress*` corrispondente viene impostato su `true` per il resto della sessione. Tutti e cinque i marcatori sono segnalati alla chiamata di chiusura.

### Indicatore di avanzamento al 10% {#progress-10}

Generato quando l&#39;indicatore di riproduzione raggiunge per la prima volta il 10% della lunghezza del contenuto.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.progress10` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress10`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |

### Indicatore di progresso del 25% {#progress-25}

Generato quando l&#39;indicatore di riproduzione raggiunge per la prima volta il 25% della lunghezza del contenuto.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.progress25` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress25`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |

### Indicatore di progresso del 50% {#progress-50}

Generato quando l&#39;indicatore di riproduzione raggiunge per la prima volta il 50% della lunghezza del contenuto.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.progress50` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress50`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |

### Indicatore di progresso del 75% {#progress-75}

Generato quando l&#39;indicatore di riproduzione raggiunge per la prima volta il 75% della lunghezza del contenuto.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.progress75` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress75`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |

### Indicatore di progresso del 95% {#progress-95}

Generato quando l&#39;indicatore di riproduzione raggiunge per la prima volta il 95% della lunghezza del contenuto.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.progress95` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress95`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |

>[!IMPORTANT]
>
>I marcatori di avanzamento richiedono una lunghezza del contenuto [&#128279;](/help/reporting/dimensions/content-length.md) diversa da zero e un report accurato della testina di riproduzione. Se la lunghezza del contenuto non è impostata, è uguale a zero o non è corretta, gli indicatori possono essere attivati al momento sbagliato o non attivati affatto.
