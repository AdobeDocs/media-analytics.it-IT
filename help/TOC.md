---
product: Media Analytics
audience: utente finale
user-guide-title: Adobe Analytics per audio e video
translation-type: tm+mt
source-git-commit: d5673ea5bf96e7ea0a43d176c182423ccece6870

---


# Adobe Analytics for Audio and Video {#using}

+ [Misurazione di audio e video in Adobe Analytics](media-overview.md)
+ Opzioni di misura {#measurement-options}
   + Tracciamento cardine modulo multimediale {#mm-milestone-tracking}
      + [Panoramica delle attività cardine](measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [Migra attività cardine in Media Analytics](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [Migrazione da attività cardine a collegamento personalizzato](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + Collegamento personalizzato in Analytics {#cl-in-aa}
      + [Guida all’implementazione dei collegamenti personalizzati](measurement-options/cl-in-aa/cl-impl-guide.md)
+ Introduzione ad Analisi audio e video {#intro-to-ava}
   + [Prerequisiti](intro-to-ava/prereqs.md)
   + Percorsi di implementazione {#implementation-paths}
      + [Panoramica](intro-to-ava/implementation-paths/implementation-paths.md)
      + [Lato client](intro-to-ava/implementation-paths/client-side-path.md)
      + [Adobe Experience Platform Launch](intro-to-ava/implementation-paths/launch-path.md)
      + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
   + [Abilitazione di Audience Manager](intro-to-ava/am-enablement.md)
+ Media Analytics SDK {#sdk-implement}
   + [Download di SDK](sdk-implement/download-sdks.md)
   + Configurare e configurare {#setup}
      + [Panoramica](sdk-implement/setup/setup-overview.md)
      + [Configurare Android](sdk-implement/setup/set-up-android.md)
      + [Configurare iOS](sdk-implement/setup/set-up-ios.md)
      + [Configurare JavaScript](sdk-implement/setup/set-up-js.md)
      + [Imposta Chromecast](sdk-implement/setup/set-up-chromecast.md)
      + [Impostazione di Roku](sdk-implement/setup/set-up-roku.md)
   + Tracciare la riproduzione audio e video {#track-av-playback}
      + [Panoramica](sdk-implement/track-av-playback/track-core-overview.md)
      + Tracciamento della riproduzione audio e video di base {#track-core}
         + [Tracciare la riproduzione di base su Android](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [Tracciare la riproduzione di base su iOS](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + [Tracciare la riproduzione di base su JavaScript](sdk-implement/track-av-playback/track-core/track-core-js.md)
         + [Tracciamento della riproduzione di base su Chromecast](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [Tracciamento della riproduzione di base su Roku](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + Tracciare il buffer {#track-buffering}
         + [Tracciare il buffer su Android](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [Tracciare il buffer su iOS](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + [Tracciare il buffer in JavaScript](sdk-implement/track-av-playback/track-buffering/track-buffering-js.md)
         + [Tracciare il buffer su Chromecast](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Tracciare il buffer sul Roku](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + Ricerca traccia {#track-seeking}
         + [Ricerca di tracce su Android](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [Ricerca di tracce su iOS](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + [Tracciamento della ricerca in JavaScript](sdk-implement/track-av-playback/track-seeking/track-seeking-js.md)
         + [Ricerca traccia su Chromecast](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Ricerca traccia su Roku](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + Implementare i metadati standard {#impl-std-metadata}
         + [Implementare i metadati standard su Android](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Implementazione di metadati standard su iOS](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [Chiavi metadati iOS](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + [Implementare i metadati standard in JavaScript](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)
         + [Implementazione di metadati standard su Chromecast](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [Parametri metadati standard - Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Implementare i metadati standard su Roku](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [Parametri metadati standard - Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Track Ads {#track-ads}
      + [Panoramica](sdk-implement/track-ads/track-ads-overview.md)
      + [Tracciare annunci su Android](sdk-implement/track-ads/track-ads-android.md)
      + [Tracciare gli annunci su iOS](sdk-implement/track-ads/track-ads-ios.md)
      + [Tracciare annunci su JavaScript](sdk-implement/track-ads/track-ads-js.md)
      + [Track Ads on Chromecast](sdk-implement/track-ads/track-ads-chromecast.md)
      + [Track Ads on Roku](sdk-implement/track-ads/track-ads-roku.md)
      + Implementazione di metadati di annunci standard {#impl-std-ad-metadata}
         + [Implementazione di metadati di annunci standard su Android](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [Implementazione di metadati di annunci standard su iOS](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + [Implementazione di metadati di annunci standard in JavaScript](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-js.md)
         + [Implementazione di metadati di annunci standard su Roku](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Tracciare capitoli e segmenti {#track-chapters}
      + [Panoramica](sdk-implement/track-chapters/track-chapters-overview.md)
      + [Tracciare capitoli e segmenti su Android](sdk-implement/track-chapters/track-chapters-android.md)
      + [Tracciare capitoli e segmenti su iOS](sdk-implement/track-chapters/track-chapters-ios.md)
      + [Tracciare capitoli e segmenti in JavaScript](sdk-implement/track-chapters/track-chapters-js.md)
      + [Tracciare capitoli e segmenti su Chromecast](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [Tracciare capitoli e segmenti su Roku](sdk-implement/track-chapters/track-chapters-roku.md)
   + Qualità dell'esperienza {#track-qos}
      + [Panoramica](sdk-implement/track-qos/track-qos-overview.md)
      + [Qualità dell'esperienza su Android](sdk-implement/track-qos/track-qos-android.md)
      + [Qualità dell'esperienza su iOS](sdk-implement/track-qos/track-qos-ios.md)
      + [Monitoraggio della qualità dell'esperienza in JavaScript](sdk-implement/track-qos/track-qos-js.md)
      + [Qualità dell'esperienza su Chromecast](sdk-implement/track-qos/track-qos-chromecast.md)
      + [Qualità dell'esperienza su Roku](sdk-implement/track-qos/track-qos-roku.md)
   + Errori di tracciamento {#track-errors}
      + [Panoramica](sdk-implement/track-errors/track-errors-overview.md)
      + [Tracciare gli errori su Android](sdk-implement/track-errors/track-errors-android.md)
      + [Tracciare gli errori su iOS](sdk-implement/track-errors/track-errors-ios.md)
      + [Tracciare gli errori in JavaScript](sdk-implement/track-errors/track-errors-js.md)
      + [Tracciare gli errori in Chromecast](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Tracciare gli errori su Roku](sdk-implement/track-errors/track-errors-roku.md)
   + [Rifiuto e privacy](sdk-implement/opt-out-privacy.md)
   + Tracciamento degli scenari {#tracking-scenarios}
      + [Riproduzione VOD senza annunci](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [Riproduzione VOD con annunci pre-roll](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [Riproduzione VOD con annunci ignorati](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
      + [Riproduzione VOD con un capitolo](sdk-implement/tracking-scenarios/vod-one-chapter.md)
      + [Riproduzione VOD con un capitolo ignorato](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
      + [Riproduzione VOD con ricerca nel contenuto principale](sdk-implement/tracking-scenarios/vod-seeking.md)
      + [Riproduzione VOD con buffering](sdk-implement/tracking-scenarios/vod-buffering.md)
      + [Tracker multipli VOD in parallelo](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
      + [VOD un tracciatore per più sessioni](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
      + [Contenuto principale live](sdk-implement/tracking-scenarios/live-main-content.md)
      + [Contenuto principale live con monitoraggio sequenziale](sdk-implement/tracking-scenarios/live-sequential.md)
   + Convalida {#validation}
      + [Panoramica sulla convalida](sdk-implement/validation/validation-overview.md)
      + [Prova 1: Riproduzione standard](sdk-implement/validation/test1-standard-playback.md)
      + [Test 2: Interruzione dei media](sdk-implement/validation/test2-media-interrupt.md)
      + [Dettagli chiamata di prova](sdk-implement/validation/test-call-details.md)
      + [Descrizioni dei parametri Heartbeat](sdk-implement/validation/heartbeat-params.md)
      + Eseguire il debug {#debugging}
         + [Debug SDK](sdk-implement/validation/debugging/sdk-debugging.md)
         + [Configurare Adobe Debug](sdk-implement/validation/debugging/config-adobe-debug.md)
         + [Creare un nuovo rapporto di debug](sdk-implement/validation/debugging/create-new-debug-report.md)
         + [Debug di dashboard e report](sdk-implement/validation/debugging/debug-dash-repts.md)
   + Analisi nelle app OTT {#analytics-with-ott}
      + [Tracciare gli stati dell'app](sdk-implement/analytics-with-ott/track-app-states.md)
      + [Tracciare le azioni eseguite nell'app](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [Imposta ID utente](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT e Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT ed Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + Cookie {#cookbook}
      + [Gestione degli arresti dell’applicazione durante la riproduzione](sdk-implement/cookbook/app-interrupts.md)
      + [Risoluzione principale:riproduzione tra annunci](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [Ripresa di sessioni inattive](sdk-implement/cookbook/resuming-inactive.md)
      + [Tracciamento in SceneGraph (Roku)](sdk-implement/cookbook/sdk-track-scenegraph.md)
      + [SDK e differenze di avvio](sdk-implement/cookbook/sdk-vs-launch-qoe.md)
   + Migrazione da 1.x a 2.x di Media Analytics {#va-1x-to-2x}
      + [Panoramica sulla migrazione](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [Confronto tra codici: Da 1,x a 2,x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [Conversione API da 1.x a 2.x](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
+ API di raccolta multimediale (RESTful) {#media-collection-api}
   + [Panoramica](media-collection-api/mc-api-overview.md)
   + Riferimento API {#mc-api-ref}
      + [Richiesta sessioni](media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [Richiesta eventi](media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [Parametri di richiesta](media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [Tipi di eventi e descrizioni](media-collection-api/mc-api-ref/mc-api-event-types.md)
      + [Schemi di convalida JSON](media-collection-api/mc-api-ref/mc-api-json-validation.md)
   + Implementazione dell'API {#mc-api-impl}
      + [Guida introduttiva](media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [Impostazione del tipo di richiesta HTTP nel lettore](media-collection-api/mc-api-impl/mc-api-set-http-req.md)
      + [Ottenimento di un ID sessione](media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
      + [Implementazione di una richiesta di eventi](media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
      + [Convalida delle richieste evento](media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
      + [Invio Di Eventi Ping](media-collection-api/mc-api-impl/mc-api-sed-pings.md)
      + [Invio di dati QoE](media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
      + [Supporto per metadati personalizzati](media-collection-api/mc-api-impl/mc-api-custom-meta.md)
      + [Condizioni di timeout](media-collection-api/mc-api-impl/mc-api-timeout.md)
      + [Controllo dell'ordine degli eventi](media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
      + [Eventi in coda quando la risposta delle sessioni è lenta](media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Tempistiche per il tracciamento dei file multimediali {#mc-api-timelines}
      + [Timeline 1 - Visualizzazione alla fine del contenuto](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [Timeline 2 - Sessione di abbandono utenti](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [Timeline 3 - Capitoli](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
   + [Tracciare il contenuto scaricato](media-collection-api/track-downloaded-content.md)
+ Metriche e metadati {#metrics-and-metadata}
   + [Parametri audio e video](metrics-and-metadata/audio-video-parameters.md)
   + [Parametri annuncio](metrics-and-metadata/ad-parameters.md)
   + [Parametri capitolo](metrics-and-metadata/chapter-parameters.md)
   + [Parametri di qualità](metrics-and-metadata/quality-parameters.md)
   + [Segmenti](metrics-and-metadata/segments.md)
   + [Metriche calcolate](metrics-and-metadata/calculated-metrics.md)
+ Reporting e analisi {#media-reports}
   + [Abilitazione di Media Reports](media-reports/media-reports-enable.md)
   + Report predefiniti per file multimediali {#media-default-reports}
      + [Panoramica dei report predefiniti](media-reports/media-default-reports/default-reports-overview.md)
      + [Panoramica sui supporti](media-reports/media-default-reports/media-reports-overview.md)
      + [Dettagli supporto](media-reports/media-default-reports/media-reports-detail.md)
      + [Daypart Media](media-reports/media-default-reports/media-reports-daypart.md)
      + [Visualizzatori simultanei](media-reports/media-default-reports/media-concurrent-viewers.md)
      + [Ottenere i dati del rapporto JSON per visualizzatori simultanei](media-reports/media-default-reports/get-concurrent-json.md)
   + [Modelli di Media Workspace](media-reports/media-workspace-templates.md)
+ [Analisi federate](federated-analytics.md)
+ Risorse aggiuntive {#additional-resources}
   + [Aggiornamenti alla documentazione](additional-resources/doc-updates.md)
