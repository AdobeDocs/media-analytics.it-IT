---
product: Media Analytics
audience: utente finale
user-guide-title: Adobe Analytics for Audio and Video
translation-type: tm+mt
source-git-commit: fece711a1b58f90f834bfc12ecc35191b6c6755d

---


# Adobe Analytics for Audio and Video {#using}

+ [Misurazione di audio e video in Adobe Analytics](media-overview.md)
+ Opzioni di misurazione {#measurement-options}
   + Tracciamento milestone milestone (modulo multimediale) {#mm-milestone-tracking}
      + [Panoramica milestone (Pietra miliare)](measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [Migrare milestone to Media Analytics](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [Migrazione da milestone a Custom Link (Migrazione da pietra miliare a collegamento personalizzato)](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + Collegamento personalizzato in Analytics {#cl-in-aa}
      + [Guida all'implementazione personalizzata dei collegamenti](measurement-options/cl-in-aa/cl-impl-guide.md)
+ Introduzione ad analisi audio e video {#intro-to-ava}
   + [Prerequisiti](intro-to-ava/prereqs.md)
   + Percorsi di implementazione {#implementation-paths}
      + [Panoramica](intro-to-ava/implementation-paths/implementation-paths.md)
      + [Lato client](intro-to-ava/implementation-paths/client-side-path.md)
      + [Adobe Experience Platform Launch](intro-to-ava/implementation-paths/launch-path.md)
      + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
   + [Abilitazione Audience Manager](intro-to-ava/am-enablement.md)
+ SDK di Media Analytics {#sdk-implement}
   + [Scaricare gli SDK](sdk-implement/download-sdks.md)
   + Configurare e configurare {#setup}
      + [Panoramica](sdk-implement/setup/setup-overview.md)
      + [Configurare Android](sdk-implement/setup/set-up-android.md)
      + [Configurare iOS](sdk-implement/setup/set-up-ios.md)
      + [Configurare javascript](sdk-implement/setup/set-up-js.md)
      + [Configurare Chromecast](sdk-implement/setup/set-up-chromecast.md)
      + [Set Up Roku](sdk-implement/setup/set-up-roku.md)
   + Tenere traccia della riproduzione audio e video {#track-av-playback}
      + [Panoramica](sdk-implement/track-av-playback/track-core-overview.md)
      + Traccia audio di base e riproduzione video {#track-core}
         + [Tracciare la riproduzione di base su Android](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [Tracciare la riproduzione di base su iOS](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + [Tracciare la riproduzione di base su javascript](sdk-implement/track-av-playback/track-core/track-core-js.md)
         + [Tracciare Core Playback su Chromecast](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [Tracciare Core Playback su Roku](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + Tenere traccia del buffering {#track-buffering}
         + [Tracciare il buffering su Android](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [Tracciare il buffering su iOS](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + [Tenere traccia del buffering in javascript](sdk-implement/track-av-playback/track-buffering/track-buffering-js.md)
         + [Traccia buffering su Chromecast](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Tracciare il buffering su Roku](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + Ricerca tracciamento {#track-seeking}
         + [Traccia ricerca su Android](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [Tracciare la ricerca su iOS](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + [Traccia ricerca su javascript](sdk-implement/track-av-playback/track-seeking/track-seeking-js.md)
         + [Traccia ricerca su Chromecast](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Traccia ricerca su Roku](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + Implementare i metadati standard {#impl-std-metadata}
         + [Implementare i metadati standard su Android](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Implementare i metadati standard su iOS](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [Chiavi metadati iOS](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + [Implementazione di metadati standard in javascript](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)
         + [Implementare i metadati standard su Chromecast](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [Parametri metadati standard - Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Implementare i metadati standard su Roku](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [Parametri metadati standard - Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Annunci di tracciamento {#track-ads}
      + [Panoramica](sdk-implement/track-ads/track-ads-overview.md)
      + [Tracciamento annunci su Android](sdk-implement/track-ads/track-ads-android.md)
      + [Tracciamento annunci su iOS](sdk-implement/track-ads/track-ads-ios.md)
      + [Tracciamento annunci su javascript](sdk-implement/track-ads/track-ads-js.md)
      + [Tracciamento annunci su Chromecast](sdk-implement/track-ads/track-ads-chromecast.md)
      + [Tracciare annunci su Roku](sdk-implement/track-ads/track-ads-roku.md)
      + Implementare i metadati degli annunci standard {#impl-std-ad-metadata}
         + [Implementare i metadati degli annunci standard su Android](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [Implementare i metadati degli annunci standard su iOS](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + [Implementare i metadati degli annunci standard in javascript](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-js.md)
         + [Implementare i metadati degli annunci standard su Roku](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Tracciare capitoli e segmenti {#track-chapters}
      + [Panoramica](sdk-implement/track-chapters/track-chapters-overview.md)
      + [Tracciare capitoli e segmenti su Android](sdk-implement/track-chapters/track-chapters-android.md)
      + [Tracciare capitoli e segmenti su iOS](sdk-implement/track-chapters/track-chapters-ios.md)
      + [Tracciare capitoli e segmenti in javascript](sdk-implement/track-chapters/track-chapters-js.md)
      + [Tracciare capitoli e segmenti su Chromecast](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [Tracciare capitoli e segmenti su Roku](sdk-implement/track-chapters/track-chapters-roku.md)
   + Tracciamento della qualità dell'esperienza {#track-qos}
      + [Panoramica](sdk-implement/track-qos/track-qos-overview.md)
      + [Tracciare la qualità dell'esperienza su Android](sdk-implement/track-qos/track-qos-android.md)
      + [Tracciare la qualità dell'esperienza su iOS](sdk-implement/track-qos/track-qos-ios.md)
      + [Tracciare la qualità dell'esperienza in javascript](sdk-implement/track-qos/track-qos-js.md)
      + [Tracciare la qualità dell'esperienza su Chromecast](sdk-implement/track-qos/track-qos-chromecast.md)
      + [Tracciare la qualità dell'esperienza su Roku](sdk-implement/track-qos/track-qos-roku.md)
   + Errori di tracciamento {#track-errors}
      + [Panoramica](sdk-implement/track-errors/track-errors-overview.md)
      + [Tenere traccia degli errori su Android](sdk-implement/track-errors/track-errors-android.md)
      + [Tenere traccia degli errori in iOS](sdk-implement/track-errors/track-errors-ios.md)
      + [Tenere traccia degli errori in javascript](sdk-implement/track-errors/track-errors-js.md)
      + [Tenere traccia degli errori su Chromecast](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Tenere traccia degli errori su Roku](sdk-implement/track-errors/track-errors-roku.md)
   + [Rinuncia e privacy](sdk-implement/opt-out-privacy.md)
   + Scenari di tracciamento {#tracking-scenarios}
      + [Riproduzione VOD senza annunci](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [Riproduzione VOD con annunci predefiniti](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [Riproduzione VOD con annunci ignorati](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
      + [Riproduzione VOD con un capitolo](sdk-implement/tracking-scenarios/vod-one-chapter.md)
      + [Riproduzione VOD con un capitolo ignorato](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
      + [Riproduzione VOD con ricerca nel contenuto principale](sdk-implement/tracking-scenarios/vod-seeking.md)
      + [Riproduzione VOD con buffering](sdk-implement/tracking-scenarios/vod-buffering.md)
      + [Più tracciatori VOD in parallelo](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
      + [VOD un tracciatore per più sessioni](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
      + [Contenuto principale live](sdk-implement/tracking-scenarios/live-main-content.md)
      + [Contenuto principale live con tracciamento sequenziale](sdk-implement/tracking-scenarios/live-sequential.md)
   + Convalida {#validation}
      + [Panoramica sulla convalida](sdk-implement/validation/validation-overview.md)
      + [Test 1: Riproduzione standard](sdk-implement/validation/test1-standard-playback.md)
      + [Test 2: Interruzione file multimediali](sdk-implement/validation/test2-media-interrupt.md)
      + [Test Call Details](sdk-implement/validation/test-call-details.md)
      + [Descrizioni parametri heartbeat](sdk-implement/validation/heartbeat-params.md)
      + Eseguire il debug {#debugging}
         + [Debug SDK](sdk-implement/validation/debugging/sdk-debugging.md)
         + [Configurare Adobe Debug](sdk-implement/validation/debugging/config-adobe-debug.md)
         + [Creare un nuovo rapporto debug](sdk-implement/validation/debugging/create-new-debug-report.md)
         + [Dashboard e rapporti di debug](sdk-implement/validation/debugging/debug-dash-repts.md)
   + Analytics in OTT Apps {#analytics-with-ott}
      + [Tracciare gli stati dell'app](sdk-implement/analytics-with-ott/track-app-states.md)
      + [Tracciare le azioni eseguite nell'app](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [Imposta ID utente](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT e Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT e Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + Procedure {#cookbook}
      + [La gestione dell'applicazione viene interrotta durante la riproduzione](sdk-implement/cookbook/app-interrupts.md)
      + [Risoluzione principale: riproduzione tra annunci](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [Ripresa delle sessioni inattive](sdk-implement/cookbook/resuming-inactive.md)
      + [Tracciamento in scenegraph (Roku)](sdk-implement/cookbook/sdk-track-scenegraph.md)
      + [Differenze SDK e Launch](sdk-implement/cookbook/sdk-vs-launch-qoe.md)
   + Migrazione da Media Analytics 1. x alla 2. x {#va-1x-to-2x}
      + [Panoramica sulla migrazione](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [Confronto dei codici: Da 1. x a 2. x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [Conversione da 1. x a 2. x](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
+ API Media Collection (restful) {#media-collection-api}
   + [Panoramica](media-collection-api/mc-api-overview.md)
   + Riferimento API {#mc-api-ref}
      + [Richiesta sessioni](media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [Richiesta eventi](media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [Parametri di richiesta](media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [Tipi di evento e descrizioni](media-collection-api/mc-api-ref/mc-api-event-types.md)
      + [Schemi di convalida JSON](media-collection-api/mc-api-ref/mc-api-json-validation.md)
   + Implementazione dell'API {#mc-api-impl}
      + [Avvio rapido](media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [Impostazione del tipo di richiesta HTTP nel lettore](media-collection-api/mc-api-impl/mc-api-set-http-req.md)
      + [Ottenimento di un ID sessione](media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
      + [Implementazione di una richiesta eventi](media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
      + [Convalida delle richieste evento](media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
      + [Invio di eventi di ping](media-collection-api/mc-api-impl/mc-api-sed-pings.md)
      + [Invio di dati qoe](media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
      + [Supporto per metadati personalizzati](media-collection-api/mc-api-impl/mc-api-custom-meta.md)
      + [Condizioni di timeout](media-collection-api/mc-api-impl/mc-api-timeout.md)
      + [Controllo dell'ordine degli eventi](media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
      + [Invio in coda di eventi quando la risposta delle sessioni è lenta](media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Timeline tracciamento della timeline {#mc-api-timelines}
      + [Timeline 1 - Visualizza alla fine del contenuto](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [Timeline 2 - Sessione utenti abbandonati](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [Timeline 3 - Capitoli](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
   + [Tracciamento del contenuto scaricato](media-collection-api/track-downloaded-content.md)
+ Metriche e metadati {#metrics-and-metadata}
   + [Parametri audio e video](metrics-and-metadata/audio-video-parameters.md)
   + [Parametri annuncio](metrics-and-metadata/ad-parameters.md)
   + [Parametri capitolo](metrics-and-metadata/chapter-parameters.md)
   + [Parametri di qualità](metrics-and-metadata/quality-parameters.md)
   + [Segmenti](metrics-and-metadata/segments.md)
   + [Metriche calcolate](metrics-and-metadata/calculated-metrics.md)
+ Reporting e analisi {#media-reports}
   + [Abilitazione rapporti media](media-reports/media-reports-enable.md)
   + Report predefiniti per file multimediali {#media-default-reports}
      + [Panoramica report predefiniti](media-reports/media-default-reports/default-reports-overview.md)
      + [Panoramica file multimediali](media-reports/media-default-reports/media-reports-overview.md)
      + [Dettagli file multimediali](media-reports/media-default-reports/media-reports-detail.md)
      + [Media giornaliero](media-reports/media-default-reports/media-reports-daypart.md)
      + [Visualizzatori simultanei](media-reports/media-default-reports/media-concurrent-viewers.md)
      + [Ottenere i dati dei rapporti JSON per visualizzatori simultanei](media-reports/media-default-reports/get-concurrent-json.md)
   + [Modelli Workspace](media-reports/media-workspace-templates.md)
+ [Analisi federate](federated-analytics.md)
+ Risorse aggiuntive {#additional-resources}
   + [Aggiornamenti alla documentazione](additional-resources/doc-updates.md)
