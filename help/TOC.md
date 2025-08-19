---
product: adobe analytics
audience: end-user
user-guide-title: Guida ai servizi per contenuti multimediali in streaming
breadcrumb-title: Guida ai servizi per contenuti multimediali in streaming
user-guide-description: Implementare servizi multimediali in streaming. Gli argomenti trattati comprendono Media SDK e Media Collection API.
sub-product: media analytics
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 72%

---


# Guida ai servizi per contenuti multimediali in streaming {#using}

+ [guida ai servizi multimediali di streaming di Adobe](media-overview.md)
+ Note sulla versione {#release-notes}
   + [Note sulla versione di Streaming Media Services](additional-resources/release-notes.md)
+ Introduzione {#getting-started}
   + [Prerequisiti](getting-started/prereqs.md)
   + [Dispositivi supportati](getting-started/supported-devices.md)
   + [Documentazione sull’implementazione di Streaming Media Services](getting-started/implementation-documentation.md)
   + [SDK, librerie ed estensioni](getting-started/download-sdks.md)
   + Fine del supporto {#end-of-support}
      + [Fine del supporto di Mobile SDK di Media Analytics](additional-resources/end-of-support-faqs.md)
      + Migrazione da Media SDK a Launch precedente {#sdk-to-launch}
         + [Panoramica](legacy/sdk-to-launch/sdk-to-launch-migration.md)
         + [Android - da Media SDK a Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS - da Media SDK a Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JavaScript - da Media SDK a Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ Implementazione {#implementation}
   + [Panoramica sull’implementazione](implementation/overview.md)
   + Implementazioni di Edge (consigliato) {#edge-recommended}
      + [Prerequisiti](/help/implementation/edge/prerequisites-edge.md)
      + SDK/estensione di Media Edge {#media-edge-sdk}
         + [Configurazione di SDK/estensioni di Media Edge](/help/implementation/edge/implementation-edge.md)
         + [Media Edge Web SDK](/help/implementation/edge/edge-web-sdk.md)
         + [SDK mobile di Media Edge](/help/implementation/edge/edge-mobile-sdk.md)
      + [API di Media Edge](/help/implementation/edge/implementation-edge-api.md)
   + Implementazioni solo per Adobe Analytics {#analytics-only}
      + [Prerequisiti](/help/implementation/media-sdk/setup/prerequisites-analytics.md)
      + Media SDK/Estensione {#media-sdk}
         + [JavaScript Web SDK](implementation/media-sdk/setup/web-implementation.md)
         + [Estensione Media Analytics](implementation/media-sdk/setup/web-implementation-tags.md)
         + [SDK per dispositivi mobili](implementation/media-sdk/setup/mobile-implementation.md)
         + SDK OTT {#ott-setup}
            + [Installare l’SDK di Chromecast](implementation/media-sdk/setup/set-up-chromecast.md)
            + [Installare l’SDK di Roku](implementation/media-sdk/setup/set-up-roku.md)
      + API Media Collection - Implementazione {#streaming-media-apis}
         + [Media Collection](implementation/media-collection-api/mc-api-overview.md)
         + [Guida introduttiva sull’API](implementation/media-collection-api/mc-api-impl/mc-api-quick-start.md)
         + [Richiesta sessioni ](implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)
         + [Richiesta eventi ](implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)
         + [Parametri di richiesta ](implementation/media-collection-api/mc-api-ref/mc-api-req-params.md)
         + [Tipi di eventi e descrizioni ](implementation/media-collection-api/mc-api-ref/mc-api-event-types.md)
         + Implementazione dell’API {#mc-api-impl}
            + [Impostazione del tipo di richiesta HTTP nel lettore](implementation/media-collection-api/mc-api-impl/mc-api-set-http-req.md)
            + [Ottenimento di un ID sessione ](implementation/media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
            + [Implementazione di una richiesta di eventi ](implementation/media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
            + [Schemi di convalida JSON ](implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md)
            + [Convalida delle richieste evento ](implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
            + [Invio di eventi ping ](implementation/media-collection-api/mc-api-impl/mc-api-sed-pings.md)
            + [Invio di dati QoE ](implementation/media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
            + [Supporto per metadati personalizzati ](implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)
            + [Condizioni di timeout ](implementation/media-collection-api/mc-api-impl/mc-api-timeout.md)
            + [Controllo dell’ordine degli eventi ](implementation/media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
            + [Eventi in coda quando la risposta delle sessioni è lenta ](implementation/media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Variabili {#variables}
      + [Parametri di Streaming Media](implementation/variables/audio-video-parameters.md)
      + [Parametri annuncio](implementation/variables/ad-parameters.md)
      + [Parametri per i capitoli](implementation/variables/chapter-parameters.md)
      + [Parametri per lo stato del lettore](implementation/variables/player-state-parameters.md)
      + [Parametri per la qualità](implementation/variables/quality-parameters.md)
      + [Metriche calcolate ](implementation/variables/calculated-metrics.md)
+ Reporting {#media-reports}
   + [Abilitazione di rapporti sui contenuti multimediali ](reporting/media-reports-enable.md)
   + Pannelli multimediali in Workspace {#media-workspace-panels}
      + [Pannello Pubblico medio per minuto](reporting/workspace/average-minute-audience.md)
      + [Pannello Visualizzatori simultanei di contenuti multimediali](reporting/workspace/media-concurrent-viewers-overview.md)
      + [Pannello Tempo trascorso su contenuti multimediali](reporting/workspace/media-playback-time-spent.md)
   + [Rapporti multimediali in Workspace](reporting/workspace/media-workspace-templates.md)
   + [Segmenti multimediali](reporting/segments.md)
   + Rapporti multimediali predefiniti {#media-default-reports}
      + [Panoramica dei rapporti predefiniti](reporting/reports-and-analytics/default-reports-overview.md)
      + [Panoramica dei contenuti multimediali](reporting/reports-and-analytics/media-reports-overview.md)
      + [Dettagli contenuti multimediali](reporting/reports-and-analytics/media-reports-detail.md)
      + [Report Media Daypart](reporting/reports-and-analytics/media-reports-daypart.md)
      + [Rapporto sui visualizzatori simultanei di contenuti multimediali](reporting/reports-and-analytics/media-concurrent-viewers-reports.md)
   + API Media {#media-api}
      + [Ottieni dati visualizzatori simultanei](reporting/reports-and-analytics/get-concurrent-json20.md)
      + [Ottieni dati sul tempo di riproduzione multimediale trascorso](reporting/reports-and-analytics/get-mediaplaybacktimespent-json20.md)
+ Casi di utilizzo {#media-use-cases}
   + [Casi d’uso di Media SDK](use-cases/cookbook/sdk-cookbook-overview.md)
   + Tracciamento dello stato del lettore {#player-state-tracking}
      + [Panoramica ](use-cases/player-state-tracking/player-state-overview.md)
      + [Stati standard e personalizzati](use-cases/player-state-tracking/standard-and-custom-states.md)
      + [Implementazione e reporting](use-cases/player-state-tracking/implementation-and-reporting.md)
      + [Tracciamento di più stati del lettore](use-cases/player-state-tracking/multiple-player-states.md)
      + [Esempi di tracciamento dello stato del lettore](use-cases/player-state-tracking/player-state-examples.md)
   + [Tracciare i contenuti scaricati ](use-cases/track-downloaded-content.md)
   + [Federated Media](use-cases/federated-media.md)
   + [Gestione degli arresti dell’applicazione durante la riproduzione](use-cases/cookbook/app-interrupts.md)
   + [Attribuzione flusso multimediale](use-cases/media-analytics-cookbook/media-dimensions.md)
   + Migrazione dei campi XDM per il connettore di origine di Analytics {#xdm-updates}
      + [Aggiorna il connettore di origine ai nuovi campi XDM Streaming Media](/help/use-cases/xdm-updates/updated-xdm-fields.md)
      + [Migrare tipi di pubblico](/help/use-cases/xdm-updates/migrate-audiences.md)
      + [Migra configurazione CJA](/help/use-cases/xdm-updates/migrate-cja-setup.md)
      + [Migra preparazione dati](/help/use-cases/xdm-updates/migrate-dataprep.md)
      + [Migrare i profili](/help/use-cases/xdm-updates/migrate-profiles.md)
      + [Mappatura dei parametri multimediali](/help/use-cases/xdm-updates/parameters-mapping.md)
   + [Ripresa di sessioni inattive](use-cases/cookbook/resuming-inactive.md)
   + [Tracciamento Roku in SceneGraph](use-cases/cookbook/sdk-track-scenegraph.md)
   + [Gestione degli spazi tra gli annunci](use-cases/cookbook/fix-ad-play-ad.md)
   + Timeline {#timelines}
      + [Inizio e fine capitolo](use-cases/timelines/chapter-start-end.md)
      + [Visualizza fino alla fine del contenuto](use-cases/timelines/view-to-end-of-content.md)
      + [Abbandona la sessione](use-cases/timelines/user-abandons-session.md)
   + Utilizzare Analytics nelle app OTT {#analytics-with-ott}
      + [Tracciare gli stati dell’app ](use-cases/analytics-with-ott/track-app-states.md)
      + [Tracciare le azioni eseguite nell’app ](use-cases/analytics-with-ott/track-app-actions.md)
      + [Configurare gli ID utente ](use-cases/analytics-with-ott/set-user-ids.md)
      + [OTT e Audience Manager ](use-cases/analytics-with-ott/ott-am.md)
      + [OTT ed Experience Cloud ](use-cases/analytics-with-ott/ott-experience-cloud.md)
+ Tracciamento {#tracking}
   + [Panoramica](use-cases/track-av-playback/track-core-overview.md)
   + Tracciare la riproduzione di contenuti multimediali Core in streaming {#track-core}
      + [Tracciare la riproduzione Core in JavaScript 3.x](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
      + [Tracciare la riproduzione di base in Chromecast](use-cases/track-av-playback/track-core/track-core-chromecast.md)
      + [Tracciare la riproduzione di base in Roku](use-cases/track-av-playback/track-core/track-core-roku.md)
   + Tracciare il buffering {#track-buffering}
      + [Tracciare il buffering in JavaScript 3.x](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
      + [Tracciare il buffering in Chromecast ](use-cases/track-av-playback/track-buffering/track-buffering-chromecast.md)
      + [Tracciare il buffering in Roku](use-cases/track-av-playback/track-buffering/track-buffering-roku.md)
   + Tracciare la ricerca {#track-seeking}
      + [Tracciare la ricerca in JavaScript 3.x](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
      + [Tracciare la ricerca in Chromecast](use-cases/track-av-playback/track-seeking/track-seeking-chromecast.md)
      + [Tracciare la ricerca in Roku](use-cases/track-av-playback/track-seeking/track-seeking-roku.md)
   + Implementare metadati standard {#impl-std-metadata}
      + [Implementare metadati standard in JavaScript 3.x](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
      + [Implementare metadati standard in Chromecast](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
      + [Parametri metadati standard - Chromecast](use-cases/track-av-playback/impl-std-metadata/chromecast-metadata.md)
      + [Implementare metadati standard in Roku](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
      + [Parametri metadati standard - Roku](use-cases/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Tracciare gli annunci {#track-ads}
      + [Panoramica](use-cases/track-ads/track-ads-overview.md)
      + [Tracciare gli annunci in JavaScript 3.x](use-cases/track-ads/track-ads-js/track-ads-js3.md)
      + [Tracciare gli annunci in Chromecast](use-cases/track-ads/track-ads-chromecast.md)
      + [Tracciare gli annunci in Roku](use-cases/track-ads/track-ads-roku.md)
      + Implementare metadati standard di annunci {#impl-std-ad-metadata}
         + [Implementare metadati standard di annunci in JavaScript 3.x](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [Implementare metadati standard di annunci in Roku](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Tracciamento capitoli e segmenti {#track-chapters}
      + [Panoramica](use-cases/track-chapters/track-chapters-overview.md)
      + [Tracciare capitoli e segmenti in JavaScript 3.x](use-cases/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [Tracciare capitoli e segmenti in Chromecast](use-cases/track-chapters/track-chapters-chromecast.md)
      + [Tracciare capitoli e segmenti in Roku](use-cases/track-chapters/track-chapters-roku.md)
   + Tracciamento qualità dell’esperienza {#track-qos}
      + [Panoramica](use-cases/track-qos/track-qos-overview.md)
      + [Tracciare la qualità dell’esperienza in JavaScript 3.x](use-cases/track-qos/track-qos-js/track-qos-js3.md)
      + [Tracciare la qualità dell’esperienza in Chromecast](use-cases/track-qos/track-qos-chromecast.md)
      + [Tracciare la qualità dell’esperienza in Roku](use-cases/track-qos/track-qos-roku.md)
   + Tracciamento errori {#track-errors}
      + [Panoramica](use-cases/track-errors/track-errors-overview.md)
      + [Tracciare gli errori in JavaScript 3.x](use-cases/track-errors/track-errors-js/track-errors-js3.md)
      + [Tracciare gli errori in Chromecast](use-cases/track-errors/track-errors-chromecast.md)
      + [Tracciare gli errori in Roku](use-cases/track-errors/track-errors-roku.md)
+ Privacy e sicurezza {#streaming-media-privacy}
   + [Impostazioni di privacy e rinuncia](privacy/opt-out-privacy.md)
   + [Sicurezza](privacy/security.md)
+ Implementazioni legacy {#legacy-implementations}
   + [Legacy - Panoramica](legacy/setup/legacy-setup-overview.md)
   + [Legacy - Download degli SDK](legacy/legacy-download-sdks.md)
   + Legacy - Media SDK {#legacy-media-sdks}
      + [Legacy - Panoramica di Media SDK](legacy/media-sdk/setup/setup-overview.md)
      + [Configurazione Android ](legacy/media-sdk/setup/set-up-android.md)
      + [Configurazione iOS ](legacy/media-sdk/setup/set-up-ios.md)
      + Configurare JavaScript {#setup-javascript}
         + [Configurare JavaScript 2.x](legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
   + [Informazioni sulla misurazione con Heartbeat](legacy/heartbeat-measurement.md)
   + [Adobe Primetime](legacy/intro-to-ava/implementation-paths/primetime-path.md)
   + [Abilitazione di Adobe Audience Management](legacy/intro-to-ava/am-enablement.md)
   + [Implementazione del collegamento personalizzato](legacy/measurement-options/cl-in-aa/cl-impl-guide.md)
   + Tracciamento Milestone legacy {#legacy-milestone-tracking}
      + [Tracciamento Milestone legacy](legacy/measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [Migrazione da Milestone a VA](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [Migrazione da Milestone a CL](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + Convalida {#validation}
      + [Panoramica sulla convalida](legacy/validation/validation-overview.md)
      + [Prova 1: riproduzione standard](legacy/validation/test1-standard-playback.md)
      + [Prova 2: interruzione del contenuto multimediale](legacy/validation/test2-media-interrupt.md)
      + [Dettagli della chiamata di prova ](legacy/validation/test-call-details.md)
      + [Descrizioni dei parametri Heartbeat](legacy/validation/heartbeat-params.md)
      + Eseguire il debug {#debugging}
         + [Debug di SDK ](legacy/validation/debugging/sdk-debugging.md)
   + [Migrazione legacy: da VHL 1.x a VHL 2.x](legacy/va-1x-to-2x/mig-1x-2x-overview.md)
   + [Confronto tra codici v1.x e v2.x](legacy/va-1x-to-2x/code-comparison-1x-2x.md)
   + [API di tracciamento da 1x a 2x](legacy/va-1x-to-2x/1x-2x-api-change.md)
   + [Legacy - Introduzione ad AVA](legacy/intro-to-ava/implementation-paths/implementation-paths.md)
   + [Percorso lato client](legacy/intro-to-ava/implementation-paths/client-side-path.md)
   + Tracciamento legacy {#track-av-playback}
      + [Tracciare la riproduzione di base su Android](use-cases/track-av-playback/track-core/track-core-android.md)
      + [Tracciare la riproduzione di base su iOS](use-cases/track-av-playback/track-core/track-core-ios.md)
      + Tracciamento riproduzione core in JavaScript {#track-core-javascript}
         + [Tracciare la riproduzione Core in JavaScript 2.x](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js.md)
         + [Tracciare il buffering su Android ](use-cases/track-av-playback/track-buffering/track-buffering-android.md)
         + [Tracciare il buffering su iOS ](use-cases/track-av-playback/track-buffering/track-buffering-ios.md)
         + Tracciamento buffering su JavaScript {#track-buffering-js}
            + [Tracciare il buffering in JavaScript 2.x](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
         + [Tracciare la ricerca su Android](use-cases/track-av-playback/track-seeking/track-seeking-android.md)
         + [Tracciare la ricerca su iOS](use-cases/track-av-playback/track-seeking/track-seeking-ios.md)
         + Tracciare la ricerca in JavaScript {#track-seeking-js}
            + [Tracciare la ricerca in JavaScript 2.x](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
         + [Implementare metadati standard su Android](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Implementare metadati standard su iOS](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [Chiavi metadati iOS](use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + Implementazione dei metadati standard in JavaScript {#impl-std-md-js}
            + [Implementare metadati standard in JavaScript 2.x](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
      + Tracciare gli annunci {#track-ads}
         + [Tracciare gli annunci su Android](use-cases/track-ads/track-ads-android.md)
         + [Tracciare gli annunci su iOS ](use-cases/track-ads/track-ads-ios.md)
         + Tracciamento annunci in JavaScript {#track-ads-js}
            + [Tracciare gli annunci in JavaScript 2.x ](use-cases/track-ads/track-ads-js/track-ads-js.md)
            + [Implementare metadati standard di annunci su Android](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
            + [Implementare i metadati standard di annunci su iOS](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
            + Implementare metadati standard di annunci in JavaScript {#impl-std-ad-md-js}
               + [Implementare metadati standard di annunci in JavaScript 2.x](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
      + Tracciamento capitoli e segmenti {#track-chapters}
         + [Tracciare capitoli e segmenti su Android](use-cases/track-chapters/track-chapters-android.md)
         + [Tracciare capitoli e segmenti su iOS](use-cases/track-chapters/track-chapters-ios.md)
         + Tracciamento capitoli e segmenti in JavaScript {#track-chapters-js}
            + [Tracciare capitoli e segmenti in JavaScript 2.x](use-cases/track-chapters/track-chapters-js/track-chapters-js.md)
         + [Tracciare la qualità dell’esperienza su Android](use-cases/track-qos/track-qos-android.md)
         + [Tracciare la qualità dell’esperienza su iOS](use-cases/track-qos/track-qos-ios.md)
         + Tracciamento qualità dell’esperienza su JavaScript {#track-qos-js}
            + [Tracciare la qualità dell’esperienza in JavaScript 2.x](use-cases/track-qos/track-qos-js/track-qos-js.md)
      + Tracciamento errori {#track-errors}
         + [Tracciare gli errori su Android](use-cases/track-errors/track-errors-android.md)
         + [Tracciare gli errori in iOS](use-cases/track-errors/track-errors-ios.md)
         + Tracciamento errori su JavaScript {#track-errors-js}
            + [Tracciare gli errori in JavaScript 2.x](use-cases/track-errors/track-errors-js/track-errors-js.md)
      + Tracciamento scenari {#tracking-scenarios}
         + [Riproduzione VOD senza annunci ](use-cases/tracking-scenarios/vod-no-intrs-details.md)
         + [Riproduzione VOD con annunci pre-roll ](use-cases/tracking-scenarios/vod-preroll-ads.md)
         + [Riproduzione VOD con annunci saltati ](use-cases/tracking-scenarios/vod-skipped-ads.md)
         + [Riproduzione VOD con un capitolo ](use-cases/tracking-scenarios/vod-one-chapter.md)
         + [Riproduzione VOD con un capitolo saltato ](use-cases/tracking-scenarios/vod-skipped-chapter.md)
         + [Riproduzione VOD con ricerca nel contenuto principale ](use-cases/tracking-scenarios/vod-seeking.md)
         + [Riproduzione VOD con buffering ](use-cases/tracking-scenarios/vod-buffering.md)
         + [VOD con più tracker in parallelo ](use-cases/tracking-scenarios/vod-multi-trackers.md)
         + [VOD con un tracker per più sessioni ](use-cases/tracking-scenarios/vod-multi-track-one-session.md)
         + [Contenuto principale live ](use-cases/tracking-scenarios/live-main-content.md)
         + [Contenuto principale live con tracciamento sequenziale ](use-cases/tracking-scenarios/live-sequential.md)
