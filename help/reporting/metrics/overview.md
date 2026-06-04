---
title: Panoramica delle metriche dei contenuti multimediali in streaming
description: Scopri come vengono calcolate e organizzate le metriche dei contenuti multimediali in streaming in Adobe Analytics e Customer Journey Analytics.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 3%

---


# Panoramica delle metriche dei contenuti multimediali in streaming

Le metriche in Streaming Media Analytics sono conteggi e durate basati su eventi calcolati dal backend multimediale. Il lettore multimediale invia eventi come l’inizio della sessione, la riproduzione, il ping e l’inizio dell’annuncio; il backend multimediale elabora tali eventi e finalizza i valori delle metriche nella chiamata di chiusura della sessione.

## Come vengono calcolate le metriche

Le metriche dei contenuti multimediali in streaming seguono quattro modelli di calcolo principali:

* **Flag attivati da eventi**: imposta la prima volta che un evento qualificato arriva in una sessione. Un evento [`play`](/help/implementation/events/playback/play.md) per il contenuto principale imposta il flag [[!UICONTROL Content starts]](content-starts.md); un evento [`adStart`](/help/implementation/events/ads/ad-start.md) imposta [[!UICONTROL Ad starts]](ad-starts.md). Il flag viene segnalato una volta per sessione nella chiamata di chiusura, non per evento.

* **Durate accumulate**: somma gli intervalli tra gli eventi ping mentre è attivo un particolare stato di riproduzione. [[!UICONTROL Content time spent]](content-time-spent.md) si accumula durante la riproduzione del contenuto principale; [[!UICONTROL Ad time spent]](ad-time-spent.md) si accumula durante la riproduzione di un annuncio. L’intervallo di ping consigliato da Adobe è di 10 secondi per il contenuto principale e di 1 secondo durante gli annunci, pertanto le metriche relative al tempo trascorso possono essere tanto granulari quanto l’intervallo di ping dell’implementazione.

* **Conteggi eventi**: tieni traccia delle occorrenze totali nella sessione. Le metriche di qualità come [[!UICONTROL Buffer events]](buffer-events.md), [[!UICONTROL Bitrate changes]](bitrate-changes.md), [[!UICONTROL Error events]](error-events.md) e [[!UICONTROL Pause events]](pause-events.md) contano ogni occorrenza, non solo la prima.

* **Flussi interessati**: flag a livello di sessione impostati su 1 se l&#39;evento corrispondente si è verificato in qualsiasi momento durante la sessione, indipendentemente dal numero di volte. Utilizza queste metriche per misurare la portata, mentre per misurare la gravità utilizzi la metrica del conteggio degli eventi. Ad esempio, è possibile utilizzare [[!UICONTROL Buffer impacted streams]](buffer-impacted-streams.md) per determinare la proporzione di sessioni interessate dal buffering in tutte le sessioni di riproduzione.

## Disponibilità per sistema di reporting

| Sistema di reporting | Arrivo delle metriche |
| --- | --- |
| Adobe Analytics | Compilato utilizzando [Variabili di dati di contesto](https://experienceleague.adobe.com/it/docs/analytics/implementation/vars/page-vars/contextdata). Alcune metriche compilano automaticamente gli eventi della soluzione utilizzando queste variabili di dati di contesto, mentre altre devono essere mappate a un evento personalizzato utilizzando [Regole di elaborazione](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview). Per le metriche che compilano automaticamente i valori, deve essere prima abilitata l&#39;impostazione [suite di rapporti per Streaming Media](../setup/analytics-reporting.md). |
| Customer Journey Analytics | Campi XDM in `xdm.mediaReporting.sessionDetails` e nodi correlati, originati da qualsiasi set di dati che include dati multimediali in streaming. È necessario creare ogni metrica con le impostazioni desiderate nelle [impostazioni del componente Visualizzazione dati](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview). |
| Feed dati | Le metriche vengono visualizzate nelle colonne `event_list` e `post_event_list` come ID evento. Ogni file di feed contiene un file `events.csv` contenente la ricerca di tutte le metriche, incluse quelle relative ai contenuti multimediali in streaming. |

>[!MORELIKETHIS]
>
>* [Panoramica eventi](/help/implementation/events/overview.md): gli eventi del lettore che popolano le metriche
>* [Panoramica delle variabili](/help/implementation/variables/overview.md): dati trasferiti dagli eventi ad Adobe
>* [Panoramica delle dimensioni](/help/reporting/dimensions/overview.md): dimensioni di reporting popolate dalle variabili
