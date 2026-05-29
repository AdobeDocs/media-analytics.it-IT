---
title: Panoramica delle dimensioni dei contenuti multimediali in streaming
description: Scopri come le dimensioni dei contenuti multimediali in streaming vengono popolate e organizzate in Adobe Analytics e Customer Journey Analytics.
feature: Dimensions
role: User, Admin
source-git-commit: 3dbbd5228fcd91cf78c0597dea656c06f367dd40
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 6%

---


# Panoramica delle dimensioni dei contenuti multimediali in streaming

Le dimensioni in Streaming Media Analytics consentono di suddividere e filtrare le metriche in base al nome del contenuto, al tipo di flusso, al nome dell’annuncio e a dozzine di altri attributi. La maggior parte è impostata dal lettore all’inizio della sessione e portata a termine alla chiusura della sessione.

## Compilazione delle dimensioni

Le dimensioni dei contenuti multimediali in streaming seguono tre pattern di popolazione principali:

* **Fornito dal lettore multimediale**: origine della maggior parte delle dimensioni. Il lettore invia questi valori nella chiamata [Inizio sessione](/help/implementation/events/session/session-start.md) e il backend multimediale li allega a ogni evento successivo nella sessione. Ciò che il lettore invia all’inizio della sessione è ciò che appare nei rapporti. Gli esempi includono [[!UICONTROL Stream type]](/help/reporting/dimensions/stream-type.md), [[!UICONTROL Content name]](/help/reporting/dimensions/content-name.md) e [[!UICONTROL Content length]](/help/reporting/dimensions/content-length.md).

* **Valori derivati**: dimensioni calcolate dal back-end del contenuto multimediale in base allo stato di riproduzione accumulato anziché in base al valore fornito dal lettore. [[!UICONTROL Content segment]](/help/reporting/dimensions/content-segment.md) viene calcolato dalla posizione della testina di riproduzione nel corso della riproduzione. [[!UICONTROL Media path]](/help/reporting/dimensions/media-path.md) tiene traccia delle transizioni tra il contenuto e gli stati degli annunci durante la sessione. Queste dimensioni non possono essere ignorate dal lettore.

* **Classificazioni**: facoltativo. Invece di popolare dimensioni separate, puoi gestire i dati di classificazione utilizzando [Set di classificazione](https://experienceleague.adobe.com/it/docs/analytics/components/classifications/sets/overview) (Adobe Analytics) o [Set di dati di ricerca](https://experienceleague.adobe.com/it/docs/analytics-platform/using/compare-aa-cja/upgrade-to-cja/create-datasets/cja-upgrade-dataset-lookup) (Customer Journey Analytics).

## Disponibilità per sistema di reporting

| Sistema di reporting | Come arrivano le dimensioni |
| --- | --- |
| Adobe Analytics | Compilato utilizzando [Variabili di dati di contesto](https://experienceleague.adobe.com/it/docs/analytics/implementation/vars/page-vars/contextdata). Alcune dimensioni compilano automaticamente le dimensioni utilizzando queste variabili di dati di contesto, mentre altre devono essere compilate utilizzando [Regole di elaborazione](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview). Le dimensioni che compilano automaticamente i valori devono prima aver abilitato le rispettive impostazioni della suite di rapporti [Streaming Media](../../implementation/media-sdk/setup/media-reports-enable.md). |
| Customer Journey Analytics | Campi XDM in genere in `xdm.mediaReporting.sessionDetails`, originati da qualsiasi set di dati che include dati multimediali in streaming. È necessario creare ogni dimensione con le impostazioni desiderate nelle [impostazioni del componente Visualizzazione dati](https://experienceleague.adobe.com/it/docs/analytics-platform/using/cja-dataviews/component-settings/overview). |
| Feed dati | Le dimensioni popolate automaticamente hanno nomi di colonna propri del feed di dati (come `videostreamtype`, `videoname` o `videolength`). Le dimensioni che richiedono regole di elaborazione utilizzano i nomi di colonna `evar`. |
| Audience Manager | Dati contestuali inoltrati da Adobe Analytics. Disponibile solo quando è configurato l’inoltro lato server da Analytics ad Audience Manager. |

>[!MORELIKETHIS]
>
>* [Panoramica eventi](/help/implementation/events/overview.md): eventi del lettore che popolano le dimensioni
>* [Panoramica delle variabili](/help/implementation/variables/overview.md): dati trasferiti dagli eventi ad Adobe
>* [Panoramica delle metriche](/help/reporting/metrics/overview.md): le metriche di reporting compilate dalle variabili
