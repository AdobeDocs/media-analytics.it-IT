---
audience: end-user
user-guide-title: ' Adobe Analytics per streaming multimediale'
breadcrumb-title: Guida all'analisi dei supporti multimediali
user-guide-description: Implementa Analytics sulle sorgenti audio o video. Gli argomenti trattati comprendono Media SDK e Media Collection API.
product: adobe analytics
sub-product: media analytics
translation-type: tm+mt
source-git-commit: da13db682f859cfd176a5ab379b7a0a947dc0e3a
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 96%

---


#  Adobe Analytics per streaming multimediale {#using}

+ [Misurazione dello streaming multimediale in  Adobe Analytics](media-overview.md)
+ [Dispositivi e piattaforme supportati](measurement-options/supported-devices.md)
+ Introduzione a Streaming Media Analytics {#intro-to-ava}
   + [Prerequisiti](intro-to-ava/prereqs.md)
   + Percorsi di implementazione {#implementation-paths}
      + [Panoramica](intro-to-ava/implementation-paths/implementation-paths.md)
      + [Lato client](intro-to-ava/implementation-paths/client-side-path.md)
      + Altri percorsi di implementazione {#other-paths}
         + Tracciamento modulo multimediale Milestone {#mm-milestone-tracking}
            + [Panoramica su Milestone](measurement-options/mm-milestone-tracking/milestone-overview.md)
            + [Migrazione da Milestone a Media Analytics](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
            + [Migrazione da Milestone a Custom Link](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
         + Custom Link in Analytics {#cl-in-aa}
            + [Guida all’implementazione di Custom Link](measurement-options/cl-in-aa/cl-impl-guide.md)
         + Primetime {#primetime}
            + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
         + [Abilitazione di Audience Manager](intro-to-ava/am-enablement.md)
+ SDK Media Analytics {#sdk-implement}
   + [Domande frequenti sull’SDK di Media Analytics riguardanti la fine del supporto](sdk-implement/end-of-support-faqs.md)
   + [Scaricare gli SDK](sdk-implement/download-sdks.md)
   + Installazione e configurazione {#setup}
      + [Panoramica](sdk-implement/setup/setup-overview.md)
      + [Configurazione Android](sdk-implement/setup/set-up-android.md)
      + [Configurazione iOS](sdk-implement/setup/set-up-ios.md)
      + Configurazione JavaScript {#setup-javascript}
         + [Configurazione JavaScript 2.x](sdk-implement/setup/setup-javascript/set-up-js-2.md)
         + [Configurazione JavaScript 3.x](sdk-implement/setup/setup-javascript/set-up-js-3.md)
      + [Configurazione Chromecast](sdk-implement/setup/set-up-chromecast.md)
      + [Configurazione Roku](sdk-implement/setup/set-up-roku.md)
   + Track Steaming Media Playback {#track-av-playback}
      + [Panoramica](sdk-implement/track-av-playback/track-core-overview.md)
      + Track Core Steaming Media Playback {#track-core}
         + [Tracciamento riproduzione core su Android](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [Tracciamento riproduzione core su iOS](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + Tracciamento riproduzione core in JavaScript {#track-core-javascript}
            + [Tracciamento riproduzione core in JavaScript 2.x](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js.md)
            + [Tracciamento riproduzione core in JavaScript 3.x](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
         + [Tracciamento riproduzione core in Chromecast](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [Tracciamento riproduzione core su Roku](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + Tracciamento del buffering {#track-buffering}
         + [Tracciamento buffering su Android](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [Tracciamento buffering su iOS](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + Tracciamento buffering in JavaScript {#track-buffering-js}
            + [Tracciamento buffering in JavaScript 2.x](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
            + [Tracciamento buffering in JavaScript 3.x](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
         + [Tracciamento buffering in Chromecast](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Tracciamento buffering su Roku](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + Tracciamento ricerca {#track-seeking}
         + [Tracciamento ricerca su Android](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [Tracciamento ricerca su iOS](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + Tracciamento ricerca in JavaScript {#track-seeking-js}
            + [Tracciamento ricerca in JavaScript 2.x](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
            + [Tracciamento ricerca in JavaScript 3.x](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
         + [Tracciamento ricerca in Chromecast](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Tracciamento ricerca su Roku](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + Implementare metadati standard {#impl-std-metadata}
         + [Implementazione dei metadati standard su Android](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Implementazione dei metadati standard su iOS](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [Chiavi metadati iOS](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + Implementazione dei metadati standard in JavaScript {#impl-std-md-js}
            + [Implementazione dei metadati standard in JavaScript 2.x](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
            + [Implementazione dei metadati standard in JavaScript 3.x](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
         + [Implementazione dei metadati standard in Chromecast](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [Parametri metadati standard - Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Implementazione dei metadati standard su Roku](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [Parametri metadati standard - Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Tracciamento annunci {#track-ads}
      + [Panoramica](sdk-implement/track-ads/track-ads-overview.md)
      + [Tracciamento annunci su Android](sdk-implement/track-ads/track-ads-android.md)
      + [Tracciamento annunci su iOS](sdk-implement/track-ads/track-ads-ios.md)
      + Tracciamento annunci in JavaScript {#track-ads-js}
         + [Tracciamento annunci in JavaScript 2.x](sdk-implement/track-ads/track-ads-js/track-ads-js.md)
         + [Tracciamento annunci in JavaScript 3.x](sdk-implement/track-ads/track-ads-js/track-ads-js3.md)
      + [Tracciamento annunci in Chromecast](sdk-implement/track-ads/track-ads-chromecast.md)
      + [Tracciamento annunci su Roku](sdk-implement/track-ads/track-ads-roku.md)
      + Implementare metadati standard di annunci {#impl-std-ad-metadata}
         + [Implementazione dei metadati standard di annunci su Android](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [Implementazione dei metadati standard di annunci su iOS](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + Implementazione dei metadati standard di annunci in JavaScript {#impl-std-ad-md-js}
            + [Implementazione dei metadati standard di annunci in JavaScript 2.x](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
            + [Implementazione dei metadati standard di annunci in JavaScript 3.x](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [Implementazione dei metadati standard di annunci su Roku](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Tracciamento capitoli e segmenti {#track-chapters}
      + [Panoramica](sdk-implement/track-chapters/track-chapters-overview.md)
      + [Tracciamento capitoli e segmenti su Android](sdk-implement/track-chapters/track-chapters-android.md)
      + [Tracciamento capitoli e segmenti su iOS](sdk-implement/track-chapters/track-chapters-ios.md)
      + Tracciamento capitoli e segmenti in JavaScript {#track-chapters-js}
         + [Tracciamento capitoli e segmenti in JavaScript 2.x](sdk-implement/track-chapters/track-chapters-js/track-chapters-js.md)
         + [Tracciamento capitoli e segmenti in JavaScript 3.x](sdk-implement/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [Tracciamento capitoli e segmenti in Chromecast](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [Tracciamento capitoli e segmenti su Roku](sdk-implement/track-chapters/track-chapters-roku.md)
   + Tracciamento qualità dell’esperienza {#track-qos}
      + [Panoramica](sdk-implement/track-qos/track-qos-overview.md)
      + [Tracciamento qualità dell’esperienza su Android](sdk-implement/track-qos/track-qos-android.md)
      + [Tracciamento qualità dell’esperienza su iOS](sdk-implement/track-qos/track-qos-ios.md)
      + Tracciamento qualità dell’esperienza in JavaScript {#track-qos-js}
         + [Tracciamento qualità dell’esperienza in JavaScript 2.x](sdk-implement/track-qos/track-qos-js/track-qos-js.md)
         + [Tracciamento qualità dell’esperienza in JavaScript 3.x](sdk-implement/track-qos/track-qos-js/track-qos-js3.md)
      + [Tracciamento qualità dell’esperienza in Chromecast](sdk-implement/track-qos/track-qos-chromecast.md)
      + [Tracciamento qualità dell’esperienza su Roku](sdk-implement/track-qos/track-qos-roku.md)
   + Tracciamento errori {#track-errors}
      + [Panoramica](sdk-implement/track-errors/track-errors-overview.md)
      + [Tracciamento errori su Android](sdk-implement/track-errors/track-errors-android.md)
      + [Tracciamento errori su iOS](sdk-implement/track-errors/track-errors-ios.md)
      + Tracciamento errori in JavaScript {#track-errors-js}
         + [Tracciamento errori in JavaScript 2.x](sdk-implement/track-errors/track-errors-js/track-errors-js.md)
         + [Tracciamento errori in JavaScript 3.x](sdk-implement/track-errors/track-errors-js/track-errors-js3.md)
      + [Tracciamento errori in Chromecast](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Tracciamento errori su Roku](sdk-implement/track-errors/track-errors-roku.md)
   + [Rinuncia e privacy](sdk-implement/opt-out-privacy.md)
   + Tracciamento scenari {#tracking-scenarios}
      + [Riproduzione VOD senza annunci](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [Riproduzione VOD con annunci pre-scorrimento](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [Riproduzione VOD con annunci saltati](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
      + [Riproduzione VOD con un capitolo](sdk-implement/tracking-scenarios/vod-one-chapter.md)
      + [Riproduzione VOD con un capitolo saltato](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
      + [Riproduzione VOD con ricerca nel contenuto principale](sdk-implement/tracking-scenarios/vod-seeking.md)
      + [Riproduzione VOD con buffering](sdk-implement/tracking-scenarios/vod-buffering.md)
      + [Tracciamenti multipli VOD in parallelo](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
      + [VOD un tracciamento per più sessioni](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
      + [Contenuto principale live](sdk-implement/tracking-scenarios/live-main-content.md)
      + [Contenuto principale live con tracciamento sequenziale](sdk-implement/tracking-scenarios/live-sequential.md)
   + Convalida {#validation}
      + [Panoramica sulla convalida](sdk-implement/validation/validation-overview.md)
      + [Prova 1: riproduzione standard](sdk-implement/validation/test1-standard-playback.md)
      + [Prova 2: interruzione contenuto multimediale](sdk-implement/validation/test2-media-interrupt.md)
      + [Dettagli chiamata di prova](sdk-implement/validation/test-call-details.md)
      + [Descrizioni dei parametri Heartbeat](sdk-implement/validation/heartbeat-params.md)
      + Eseguire il debug {#debugging}
         + [Debug di SDK](sdk-implement/validation/debugging/sdk-debugging.md)
         + [Configurazione di Adobe Debug](sdk-implement/validation/debugging/config-adobe-debug.md)
         + [Creazione di un nuovo report di debug](sdk-implement/validation/debugging/create-new-debug-report.md)
         + [Dashboard e report di debug](sdk-implement/validation/debugging/debug-dash-repts.md)
   + Analytics nelle app OTT {#analytics-with-ott}
      + [Tracciamento stati dell’app](sdk-implement/analytics-with-ott/track-app-states.md)
      + [Tracciamento azioni eseguite nell’app](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [Configurazione ID utente](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT e Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT ed Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + Guida di riferimento dettagliata {#cookbook}
      + [Guida di riferimento SDK](sdk-implement/cookbook/sdk-cookbook-overview.md)
      + [Gestione degli arresti dell’applicazione durante la riproduzione](sdk-implement/cookbook/app-interrupts.md)
      + [Risoluzione main:play tra annunci](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [Ripresa di sessioni inattive](sdk-implement/cookbook/resuming-inactive.md)
      + [Tracciamento in SceneGraph (Roku)](sdk-implement/cookbook/sdk-track-scenegraph.md)
   + Migrazione da Media Analytics 1.x a 2.x {#va-1x-to-2x}
      + [Panoramica sulla migrazione](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [Confronto tra codici: da 1.x a 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [Conversione API da 1.x a 2.x](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
   + Migrazione dall’SDK Media Analytics a Launch {#sdk-to-launch}
      + [Migrazione dall’SDK a Launch](sdk-implement/sdk-to-launch/sdk-to-launch-migration.md)
      + Migrazione dall’SDK a Launch - Guide per piattaforma {#sdk-to-launch-migration-platforms}
         + [Android](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ API Media Collection (RESTful) {#media-collection-api}
   + [Panoramica](media-collection-api/mc-api-overview.md)
   + Riferimento API {#mc-api-ref}
      + [Richiesta sessioni](media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [Richiesta eventi](media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [Parametri di richiesta](media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [Tipi di eventi e descrizioni](media-collection-api/mc-api-ref/mc-api-event-types.md)
      + [Schemi di convalida JSON](media-collection-api/mc-api-ref/mc-api-json-validation.md)
   + Implementazione dell’API {#mc-api-impl}
      + [Guida introduttiva](media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [Impostazione del tipo di richiesta HTTP nel lettore](media-collection-api/mc-api-impl/mc-api-set-http-req.md)
      + [Ottenimento di un ID sessione](media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
      + [Implementazione di una richiesta di eventi](media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
      + [Convalida delle richieste evento](media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
      + [Invio di eventi ping](media-collection-api/mc-api-impl/mc-api-sed-pings.md)
      + [Invio di dati QoE](media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
      + [Supporto per metadati personalizzati](media-collection-api/mc-api-impl/mc-api-custom-meta.md)
      + [Condizioni di timeout](media-collection-api/mc-api-impl/mc-api-timeout.md)
      + [Controllo dell’ordine degli eventi](media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
      + [Eventi in coda quando la risposta delle sessioni è lenta](media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Timeline per il tracciamento dei file multimediali {#mc-api-timelines}
      + [Timeline 1: visualizza fino alla fine del contenuto](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [Timeline 2: utente abbandona la sessione](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [Timeline 3: capitoli](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
+ Guida di riferimento dettagliata {#media-analytics-cookbook}
   + [Guida di riferimento dettagliata](media-analytics-cookbook/media-analytics-cookbook.md)
   + [Attribuzione flusso multimediale](media-analytics-cookbook/media-dimensions.md)
+ Metriche e metadati {#metrics-and-metadata}
   + [Parametri dei supporti di streaming](metrics-and-metadata/audio-video-parameters.md)
   + [Parametri annuncio](metrics-and-metadata/ad-parameters.md)
   + [Parametri capitolo](metrics-and-metadata/chapter-parameters.md)
   + [Parametri stato del lettore](metrics-and-metadata/player-state-parameters.md)
   + [Parametri di qualità](metrics-and-metadata/quality-parameters.md)
   + [Segmenti](metrics-and-metadata/segments.md)
   + [Metriche calcolate](metrics-and-metadata/calculated-metrics.md)
+ Reporting e analisi {#media-reports}
   + [Abilitazione di report multimediali](media-reports/media-reports-enable.md)
   + Report predefiniti per contenuti multimediali {#media-default-reports}
      + [Panoramica dei report predefiniti](media-reports/media-default-reports/default-reports-overview.md)
      + [Panoramica contenuti multimediali](media-reports/media-default-reports/media-reports-overview.md)
      + [Dettagli contenuti multimediali](media-reports/media-default-reports/media-reports-detail.md)
      + [Report del dayparting dei contenuti multimediali](media-reports/media-default-reports/media-reports-daypart.md)
      + [Report dei visualizzatori simultanei di contenuti multimediali](media-reports/media-default-reports/media-concurrent-viewers.md)
   + Pannelli di Media Workspace {#media-workspace-panels}
      + [Pannello dei visualizzatori simultanei di contenuti multimediali](media-reports/media-workspace-panels/media-concurrent-viewers.md)
   + [Modelli di Media Workspace](media-reports/media-workspace-templates.md)
   + [Ottenere i dati dei visualizzatori simultanei tramite API](media-reports/media-default-reports/get-concurrent-json20.md)
+ [Tracciamento contenuto scaricato](media-collection-api/track-downloaded-content.md)
+ [Federated Analytics](federated-analytics.md)

<!-- + Basic Streaming Media Measurement for Adobe Analytics Ultimate{#basic-streaming-measurement} -->
+ Tracciamento dello stato del lettore {#player-state-tracking}
   + [Panoramica](sdk-implement/player-state-tracking/player-state-overview.md)
   + [Stati standard e personalizzati](sdk-implement/player-state-tracking/standard-and-custom-states.md)
   + [Implementazione e reporting](sdk-implement/player-state-tracking/implementation-and-reporting.md)
   + [Esempi di tracciamento dello stato del lettore](sdk-implement/player-state-tracking/player-state-examples.md)
+ Risorse aggiuntive {#additional-resources}
   + [Note sulla versione](additional-resources/doc-updates.md)
