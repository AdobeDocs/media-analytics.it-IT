---
title: Mappatura dei parametri di Media Analytics per Adobe Experience Platform e Customer Journey Analytics
description: Mappatura del percorso del campo XDM per i parametri Media Analytics utilizzati con il connettore Source di Analytics e Customer Journey Analytics.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 79203a2f-8158-44f2-83b2-146179be9180
TQID: https://experienceleague.adobe.com/ct8mDbIpg15Jzvf1MRaG4XFtuxbq-EUKPe106zyO7zQ
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 953
ht-degree: 22%

---

# Mappatura dei parametri di Media Analytics per Adobe Experience Platform e Customer Journey Analytics

Questo documento fornisce un elenco completo di tutti i parametri di Media Analytics utilizzati in Adobe Experience Platform e Customer Journey Analytics. Il suo scopo è quello di supportare l&#39;integrazione dei dati importati da Adobe Analytics a Platform tramite il [connettore Source Analytics](https://experienceleague.adobe.com/it/docs/experience-platform/sources/connectors/adobe-applications/analytics) o il [connettore Source Analytics per le classificazioni](https://experienceleague.adobe.com/it/docs/experience-platform/sources/connectors/adobe-applications/classifications), mappando ogni parametro al percorso del campo XDM corrispondente.

>[!NOTE]
>
>Questo riferimento si applica alle organizzazioni che utilizzano il [connettore di origine di Analytics](https://experienceleague.adobe.com/it/docs/experience-platform/sources/connectors/adobe-applications/analytics) per trasferire dati multimediali in streaming da Adobe Analytics a Adobe Experience Platform per l&#39;utilizzo con Customer Journey Analytics Reporting o altri servizi Platform. Queste modifiche non influiscono su Adobe Analytics come applicazione autonoma, incluse la raccolta, l’elaborazione e il reporting di dati.

## Variabili riservate di Media Analytics

A partire da ottobre 2025, il percorso del campo XDM `media.mediaTimed` utilizzato dal connettore di origine di Analytics è completamente obsoleto e sostituito da `mediaReporting`. I dati acquisiti dopo ottobre 2025 includono solo `mediaReporting` campi. I dati precedenti rimangono disponibili nel percorso del campo legacy, riportato nelle tabelle seguenti in **Campo XDM legacy**.

### Comportamento di chiamata keep-alive

Con il connettore di origine di Analytics per lo streaming multimediale, le chiamate keep-alive da Adobe Analytics ora vengono acquisite in Adobe Experience Platform. Questo può influire sulla generazione di rapporti di Customer Journey Analytics:

* **Numero sessioni**: le chiamate Keep-alive consentono di mantenere attive le sessioni utente anche senza interazioni multimediali dirette. Queste chiamate vengono generate ogni 20 minuti dopo l’ultimo evento per ogni riproduzione multimediale. Per garantire il tracciamento ottimale delle sessioni, configura la scadenza della visita in 30 minuti nella visualizzazione dati.

* **Conteggi eventi**: le chiamate keep-alive ora vengono conteggiate per la metrica Eventi di Customer Journey Analytics. Per escluderli, creare un filtro che escluda gli eventi con Tipo evento `media.keepalive`.

## Parametri per Streaming Media

| Nome campo: | Campo XDM legacy | Percorso campo XDM per reporting | Tipo di dati | Campo derivato | Note |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL Stream Type]](/help/reporting/dimensions/stream-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.streamType` | `xdm.mediaReporting.`<br>`sessionDetails.streamType` | Dimensione | [[!UICONTROL Stream Type]](/help/reporting/dimensions/stream-type.md) | |
| [[!UICONTROL Content ID]](/help/reporting/dimensions/asset-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id` | `xdm.mediaReporting.`<br>`sessionDetails.name` | Dimensione | [[!UICONTROL Content ID]](/help/reporting/dimensions/asset-id.md) | |
| [[!UICONTROL Content Length]](/help/reporting/dimensions/content-length.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`sessionDetails.length` | Dimensione | [[!UICONTROL Content Length]](/help/reporting/dimensions/content-length.md) | |
| [[!UICONTROL Content Type]](/help/reporting/dimensions/content-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastContentType` | `xdm.mediaReporting.`<br>`sessionDetails.contentType` | Dimensione | [[!UICONTROL Content Type]](/help/reporting/dimensions/content-type.md) | |
| [[!UICONTROL Media Session ID]](/help/reporting/dimensions/media-session-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails._id` | `xdm.mediaReporting.`<br>`sessionDetails.ID` | Dimensione | [[!UICONTROL Media Session ID]](/help/reporting/dimensions/media-session-id.md) | |
| [[!UICONTROL Content Player Name]](/help/reporting/dimensions/content-player-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`sessionDetails.playerName` | Dimensione | [[!UICONTROL Content Player Name]](/help/reporting/dimensions/content-player-name.md) | |
| [[!UICONTROL Content Channel]](/help/reporting/dimensions/content-channel.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastChannel` | `xdm.mediaReporting.`<br>`sessionDetails.channel` | Dimensione | [[!UICONTROL Content Channel]](/help/reporting/dimensions/content-channel.md) | |
| [[!UICONTROL Content Segment]](/help/reporting/dimensions/content-segment.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.videoSegment` | `xdm.mediaReporting.`<br>`sessionDetails.segment` | Dimensione | [[!UICONTROL Content Segment]](/help/reporting/dimensions/content-segment.md) | |
| [[!UICONTROL Content Name]](/help/reporting/dimensions/content-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._dc.title` | `xdm.mediaReporting.`<br>`sessionDetails.friendlyName` | Dimensione | [[!UICONTROL Content Name]](/help/reporting/dimensions/content-name.md) | |
| Percorso video | *Non utilizzato in AEP/CJA* | | | | Proprietà specifica di Adobe Analytics |
| [[!UICONTROL Show]](/help/reporting/dimensions/show.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.show` | Dimensione | [[!UICONTROL Show]](/help/reporting/dimensions/show.md) | |
| [[!UICONTROL Season]](/help/reporting/dimensions/season.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.season` | Dimensione | [[!UICONTROL Season]](/help/reporting/dimensions/season.md) | |
| [[!UICONTROL Episode]](/help/reporting/dimensions/episode.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.episode` | Dimensione | [[!UICONTROL Episode]](/help/reporting/dimensions/episode.md) | |
| [[!UICONTROL Genre]](/help/reporting/dimensions/genre.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Genre` | `xdm.mediaReporting.`<br>`sessionDetails.genreList` | Dimensione | non supportato | Usa campo `mediaReporting` |
| [[!UICONTROL Network]](/help/reporting/dimensions/network.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastNetwork` | `xdm.mediaReporting.`<br>`sessionDetails.network` | Dimensione | [[!UICONTROL Network]](/help/reporting/dimensions/network.md) | |
| [[!UICONTROL Show Type]](/help/reporting/dimensions/show-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.showType` | `xdm.mediaReporting.`<br>`sessionDetails.showType` | Dimensione | [[!UICONTROL Show Type]](/help/reporting/dimensions/show-type.md) | |
| [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md) | `xdm.media.mediaTimed.`<br>`idp` | `xdm.mediaReporting.`<br>`sessionDetails.mvpd` | Dimensione | [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md) | |
| [[!UICONTROL Authorized]](/help/reporting/metrics/authorized.md) | Non supportati | `xdm.mediaReporting.`<br>`sessionDetails.authorized` | Dimensione | [[!UICONTROL Authorized]](/help/reporting/metrics/authorized.md) | |
| [[!UICONTROL Day Part]](/help/reporting/dimensions/day-part.md) | Non supportati | `xdm.mediaReporting.`<br>`sessionDetails.dayPart` | Dimensione | [[!UICONTROL Day Part]](/help/reporting/dimensions/day-part.md) | |
| [[!UICONTROL Media Feed Type]](/help/reporting/dimensions/media-feed-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sourceFeed` | `xdm.mediaReporting.`<br>`sessionDetails.feed` | Dimensione | [[!UICONTROL Media Feed Type]](/help/reporting/dimensions/media-feed-type.md) | |
| [[!UICONTROL Artist]](/help/reporting/dimensions/artist.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.artist` | `xdm.mediaReporting.`<br>`sessionDetails.artist` | Dimensione | [[!UICONTROL Artist]](/help/reporting/dimensions/artist.md) | |
| [[!UICONTROL Album]](/help/reporting/dimensions/album.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.album` | `xdm.mediaReporting.`<br>`sessionDetails.album` | Dimensione | [[!UICONTROL Album]](/help/reporting/dimensions/album.md) | |
| [[!UICONTROL Label]](/help/reporting/dimensions/label.md) | Non supportati | `xdm.mediaReporting.`<br>`sessionDetails.label` | Dimensione | [[!UICONTROL Label]](/help/reporting/dimensions/label.md) | |
| [[!UICONTROL Author]](/help/reporting/dimensions/author.md) | Non supportati | `xdm.mediaReporting.`<br>`sessionDetails.author` | Dimensione | [[!UICONTROL Author]](/help/reporting/dimensions/author.md) | |
| [[!UICONTROL Station]](/help/reporting/dimensions/station.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TRSN` | `xdm.mediaReporting.`<br>`sessionDetails.station` | Dimensione | [[!UICONTROL Station]](/help/reporting/dimensions/station.md) | |
| [[!UICONTROL Publisher]](/help/reporting/dimensions/publisher.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TPUB` | `xdm.mediaReporting.`<br>`sessionDetails.publisher` | Dimensione | [[!UICONTROL Publisher]](/help/reporting/dimensions/publisher.md) | |
| [[!UICONTROL Media Starts]](/help/reporting/metrics/media-starts.md) | `xdm.media.mediaTimed.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`sessionDetails.isViewed` | Metrica | [[!UICONTROL Media Starts]](/help/reporting/metrics/media-starts.md) | |
| [[!UICONTROL Content Starts]](/help/reporting/metrics/content-starts.md) | `xdm.media.mediaTimed.`<br>`starts.value` | `xdm.mediaReporting.`<br>`sessionDetails.isPlayed` | Metrica | [[!UICONTROL Content Starts]](/help/reporting/metrics/content-starts.md) | |
| [[!UICONTROL Content Complete]](/help/reporting/metrics/content-completes.md) | `xdm.media.mediaTimed.`<br>`completes.value` | `xdm.mediaReporting.`<br>`sessionDetails.isCompleted` | Metrica | [[!UICONTROL Content Complete]](/help/reporting/metrics/content-completes.md) | |
| [[!UICONTROL Content Time Spent]](/help/reporting/metrics/content-time-spent.md) | `xdm.media.mediaTimed.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.timePlayed` | Metrica | [[!UICONTROL Content Time Spent]](/help/reporting/metrics/content-time-spent.md) | |
| [[!UICONTROL Media Time Spent]](/help/reporting/metrics/media-time-spent.md) | `xdm.media.mediaTimed.`<br>`totalTimePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.totalTimePlayed` | Metrica | [[!UICONTROL Media Time Spent]](/help/reporting/metrics/media-time-spent.md) | |
| [[!UICONTROL Unique Time Played]](/help/reporting/metrics/unique-time-played.md) | Non supportati | `xdm.mediaReporting.`<br>`sessionDetails.uniqueTimePlayed` | Metrica | [[!UICONTROL Unique Time Played]](/help/reporting/metrics/unique-time-played.md) | |
| [[!UICONTROL 10% Progress Marker]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress10.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress10` | Metrica | [[!UICONTROL 10% Progress Marker]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 25% Progress Marker]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress25.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress25` | Metrica | [[!UICONTROL 25% Progress Marker]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 50% Progress Marker]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress50.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress50` | Metrica | [[!UICONTROL 50% Progress Marker]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 75% Progress Marker]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress75.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress75` | Metrica | [[!UICONTROL 75% Progress Marker]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 95% Progress Marker]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress95.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress95` | Metrica | [[!UICONTROL 95% Progress Marker]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL Average Minute Audience]](/help/reporting/metrics/average-minute-audience.md) | Non supportati | `xdm.mediaReporting.`<br>`sessionDetails.averageMinuteAudience` | Metrica | [[!UICONTROL Average Minute Audience]](/help/reporting/metrics/average-minute-audience.md) | |
| Secondi trascorsi dall’ultima chiamata | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sessionTimeout` | `xdm.mediaReporting.`<br>`sessionDetails.secondsSinceLastCall` | Metrica | Secondi trascorsi dall’ultima chiamata | |
| [[!UICONTROL Paused Impacted Streams]](/help/reporting/metrics/paused-impacted-streams.md) | Non supportati | `xdm.mediaReporting.`<br>`sessionDetails.hasPauseImpactedStreams` | Metrica | [[!UICONTROL Paused Impacted Streams]](/help/reporting/metrics/paused-impacted-streams.md) | copriamo mediaTimed calcolando questo valore da altri eventi |
| [[!UICONTROL Pause Events]](/help/reporting/metrics/pause-events.md) | `xdm.media.mediaTimed.`<br>`pauses.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseCount` | Metrica | [[!UICONTROL Pause Events]](/help/reporting/metrics/pause-events.md) | |
| [[!UICONTROL Total Pause Duration]](/help/reporting/metrics/total-pause-duration.md) | `xdm.media.mediaTimed.`<br>`pauseTime.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseTime` | Metrica | [[!UICONTROL Total Pause Duration]](/help/reporting/metrics/total-pause-duration.md) | |
| [[!UICONTROL Content Resumes]](/help/reporting/metrics/content-resumes.md) | `xdm.media.mediaTimed.`<br>`resumes.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasResume` | Metrica | [[!UICONTROL Content Resumes]](/help/reporting/metrics/content-resumes.md) | |
| [[!UICONTROL Content Segment Views]](/help/reporting/metrics/content-segment-views.md) | `xdm.media.mediaTimed.`<br>`mediaSegmentViews.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasSegmentView` | Metrica | [[!UICONTROL Content Segment Views]](/help/reporting/metrics/content-segment-views.md) | |

## Aggiornamento dei parametri dello stato del lettore

| Nome campo: | Campo XDM legacy | Percorso campo XDM per reporting | Tipo di dati | Campo derivato | Note |
| --- | --- | --- | --- | --- | --- |
| Flussi interessati dagli stati del lettore | Non supportati | `xdm.mediaReporting.`<br>`states.isSet` | Metrica | non supportato | usa campo `mediaReporting` |
| Conteggi degli stati del lettore | Non supportati | `xdm.mediaReporting.`<br>`states.count` | Metrica | non supportato | usa campo `mediaReporting` |
| Durata totale stati del lettore | Non supportati | `xdm.mediaReporting.`<br>`states.time` | Metrica | non supportato | usa campo `mediaReporting` |
| Nome stato lettore | Non supportati | `xdm.mediaReporting.`<br>`states.name` | Dimensione | non supportato | usa campo `mediaReporting` |

## Parametri per i capitoli

| Nome campo: | Campo XDM legacy | Percorso campo XDM per reporting | Tipo di dati | Campo derivato | Note |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL Chapter]](/help/reporting/dimensions/chapter.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.chapterAssetReference._id` | `xdm.mediaReporting.`<br>`chapterDetails.ID` | Dimensione | [[!UICONTROL Chapter]](/help/reporting/dimensions/chapter.md) | |
| [[!UICONTROL Chapter Start]](/help/reporting/metrics/chapter-starts.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.impressions.value` | `xdm.mediaReporting.`<br>`chapterDetails.isStarted` | Metrica | [[!UICONTROL Chapter Start]](/help/reporting/metrics/chapter-starts.md) | |
| [[!UICONTROL Chapter Complete]](/help/reporting/metrics/chapter-completes.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.completes.value` | `xdm.mediaReporting.`<br>`chapterDetails.isCompleted` | Metrica | [[!UICONTROL Chapter Complete]](/help/reporting/metrics/chapter-completes.md) | |
| [[!UICONTROL Chapter Time Spent]](/help/reporting/metrics/chapter-time-spent.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.timePlayed.value` | `xdm.mediaReporting.`<br>`chapterDetails.timePlayed` | Metrica | [[!UICONTROL Chapter Time Spent]](/help/reporting/metrics/chapter-time-spent.md) | |

## Parametri per gli annunci

| Nome campo: | Campo XDM legacy | Percorso campo XDM per reporting | Tipo di dati | Campo derivato | Note |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL Ad ID]](/help/reporting/dimensions/ad.md) | `xdm.advertising.`<br>`adAssetReference._id` | `xdm.mediaReporting.`<br>`advertisingDetails.name` | Dimensione | [[!UICONTROL Ad ID]](/help/reporting/dimensions/ad.md) | |
| [[!UICONTROL Ad In Pod Position]](/help/reporting/dimensions/ad-in-pod-position.md) | `xdm.advertising.`<br>`adAssetViewDetails.index` | `xdm.mediaReporting.`<br>`advertisingDetails.podPosition` | Dimensione | [[!UICONTROL Ad In Pod Position]](/help/reporting/dimensions/ad-in-pod-position.md) | |
| [[!UICONTROL Ad Length]](/help/reporting/dimensions/ad-length.md) | `xdm.advertising.`<br>`adAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`advertisingDetails.length` | Metrica | [[!UICONTROL Ad Length]](/help/reporting/dimensions/ad-length.md) | |
| [[!UICONTROL Ad Player Name]](/help/reporting/dimensions/ad-player-name.md) | `xdm.advertising.`<br>`adAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`advertisingDetails.playerName` | Dimensione | [[!UICONTROL Ad Player Name]](/help/reporting/dimensions/ad-player-name.md) | |
| [[!UICONTROL Ad Break ID]](/help/reporting/dimensions/ad-pod.md) | `xdm.advertising.`<br>`adAssetViewDetails.adBreak._id` | `xdm.mediaReporting.`<br>`advertisingPodDetails.ID` | Dimensione | [[!UICONTROL Ad Break ID]](/help/reporting/dimensions/ad-pod.md) | |
| [[!UICONTROL Ad Name]](/help/reporting/dimensions/ad-name.md) | `xdm.advertising.`<br>`adAssetReference._dc.title` | `xdm.mediaReporting.`<br>`advertisingDetails.friendlyName` | Dimensione | [[!UICONTROL Ad Name]](/help/reporting/dimensions/ad-name.md) | |
| [[!UICONTROL Advertiser]](/help/reporting/dimensions/advertiser.md) | `xdm.advertising.`<br>`adAssetReference.advertiser` | `xdm.mediaReporting.`<br>`advertisingDetails.advertiser` | Dimensione | [[!UICONTROL Advertiser]](/help/reporting/dimensions/advertiser.md) | |
| [[!UICONTROL Campaign ID]](/help/reporting/dimensions/campaign-id.md) | `xdm.advertising.`<br>`adAssetReference.campaign` | `xdm.mediaReporting.`<br>`advertisingDetails.campaignID` | Dimensione | [[!UICONTROL Campaign ID]](/help/reporting/dimensions/campaign-id.md) | |
| [[!UICONTROL Ad Start]](/help/reporting/metrics/ad-starts.md) | `xdm.advertising.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isStarted` | Metrica | [[!UICONTROL Ad Start]](/help/reporting/metrics/ad-starts.md) | |
| [[!UICONTROL Ad Complete]](/help/reporting/metrics/ad-completes.md) | `xdm.advertising.`<br>`completes.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isCompleted` | Metrica | [[!UICONTROL Ad Complete]](/help/reporting/metrics/ad-completes.md) | |
| [[!UICONTROL Ad Time Spent]](/help/reporting/metrics/ad-time-spent.md) | `xdm.advertising.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`advertisingDetails.timePlayed` | Metrica | [[!UICONTROL Ad Time Spent]](/help/reporting/metrics/ad-time-spent.md) | |

## Parametri per la qualità

| Nome campo: | Campo XDM legacy | Percorso campo XDM per reporting | Tipo di dati | Campi derivati | Note |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL Average Bitrate]](/help/reporting/metrics/average-bitrate.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateAverage.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateAverage` | Entrambi | [[!UICONTROL Average Bitrate]](/help/reporting/metrics/average-bitrate.md) | |
| [[!UICONTROL Time To Start]](/help/reporting/metrics/time-to-start.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.timeToStart.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.timeToStart` | Entrambi | [[!UICONTROL Time To Start]](/help/reporting/metrics/time-to-start.md) | |
| [[!UICONTROL Dropped Frames]](/help/reporting/metrics/dropped-frames.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.droppedFrames.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.droppedFrames` | Entrambi | [[!UICONTROL Dropped Frames]](/help/reporting/metrics/dropped-frames.md) | |
| [[!UICONTROL Buffer Events]](/help/reporting/metrics/buffer-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.buffers.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferCount` | Entrambi | [[!UICONTROL Buffer Events]](/help/reporting/metrics/buffer-events.md) | |
| [[!UICONTROL Total Buffer Duration]](/help/reporting/metrics/total-buffer-duration.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bufferTime.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferTime` | Entrambi | [[!UICONTROL Total Buffer Duration]](/help/reporting/metrics/total-buffer-duration.md) | |
| [[!UICONTROL Bitrate Changes]](/help/reporting/metrics/bitrate-changes.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateChanges.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateChangeCount` | Entrambi | [[!UICONTROL Bitrate Changes]](/help/reporting/metrics/bitrate-changes.md) | |
| [[!UICONTROL Errors / Error Events]](/help/reporting/metrics/error-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.errors.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.errorCount` | Entrambi | [[!UICONTROL Errors / Error Events]](/help/reporting/metrics/error-events.md) | |
| [[!UICONTROL Player SDK Error IDs]](/help/reporting/dimensions/player-sdk-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.playerSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.playerSdkErrors` | Dimensione | non supportato | usa campo `mediaReporting` |
| [[!UICONTROL External Error IDs]](/help/reporting/dimensions/external-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.externalSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.externalErrors` | Dimensione | non supportato | usa campo `mediaReporting` |
| [[!UICONTROL Drops Before Start]](/help/reporting/metrics/drops-before-start.md) | `xdm.media.mediaTimed.`<br>`dropBeforeStarts.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.isDroppedBeforeStart` | Metrica | [[!UICONTROL Drops Before Start]](/help/reporting/metrics/drops-before-start.md) | |
| [[!UICONTROL Buffer Impacted Streams]](/help/reporting/metrics/buffer-impacted-streams.md) | Non supportati | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBufferImpactedStreams` | Metrica | [[!UICONTROL Buffer Impacted Streams]](/help/reporting/metrics/buffer-impacted-streams.md) | calcolato da altri eventi |
| [[!UICONTROL Bitrate Change Impacted Streams]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | Non supportati | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBitrateChangeImpactedStreams` | Metrica | [[!UICONTROL Bitrate Change Impacted Streams]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | calcolato da altri eventi |
| [[!UICONTROL Error Impacted Streams]](/help/reporting/metrics/error-impacted-streams.md) | Non supportati | `xdm.mediaReporting.`<br>`qoeDataDetails.hasErrorImpactedStreams` | Metrica | [[!UICONTROL Error Impacted Streams]](/help/reporting/metrics/error-impacted-streams.md) | calcolato da altri eventi |
| [[!UICONTROL Dropped Frame Impacted Streams]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | Non supportati | `xdm.mediaReporting.`<br>`qoeDataDetails.hasDroppedFrameImpactedStreams` | Metrica | [[!UICONTROL Dropped Frame Impacted Streams]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | calcolato da altri eventi |

## Classificazioni di Media Analytics

Le classificazioni di Media Analytics vengono acquisite in AEP tramite un flusso separato noto come ACDC. Ogni gruppo di classificazione elencato nella tabella seguente corrisponde a un set di dati univoco all’interno di AEP. In CJA, è necessario stabilire una connessione tra il set di dati dell’evento Media Analytics e ciascuno dei set di dati di classificazione.

### Connessione dei set di dati in Customer Journey Analytics

Per impostare la connessione in Customer Journey Analytics:

* Passare alla scheda **Connessioni** e selezionare **Crea nuova connessione**.
* Nell&#39;interfaccia Connessioni, scegli **Aggiungi set di dati** e individua il set di dati dell&#39;evento Media Analytics (utilizzato per l&#39;importazione di dati multimediali tramite ADC), insieme ai quattro set di dati di classificazione rilevanti.

### Dettagli configurazione

Per ogni set di dati di ricerca (set di dati di classificazione), configura come segue:

* **set di dati video**:
   * Chiave: `_sandbox.key`
   * Chiave corrispondente: `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   * Tipo di origine dati: `Web Data`

* **set di dati videoad**:
   * Chiave: `_sandbox.key`
   * Chiave corrispondente: `Ad ID (advertising.adAssetReference._id)`
   * Tipo di origine dati: `Web Data`

* **set di dati videoadpod**:
   * Chiave: `_sandbox.key`
   * Chiave corrispondente: `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   * Tipo di origine dati: `Web Data`

* **set di dati videochapter**:
   * Chiave: `_sandbox.key`
   * Chiave corrispondente: `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   * Tipo di origine dati: `Web Data`

### Considerazioni sul reporting

Quando lavori con i set di dati di classificazione durante il reporting, accertati di fare riferimento ai percorsi dei campi specifici della classificazione (`ACDC XDM Path`) invece dei campi XDM di Media Analytics standard.

## Tabella classificazioni

| Nome classificazione (gruppo) | Nome campo: | Percorso ACDC XDM |
| --- | --- | --- |
| video | ID chiave/risorsa | `xdm.<_sandbox>.key` |
| video | Lunghezza video | `xdm.<_sandbox>.video_length` |
| video | Nome del video | `xdm.<_sandbox>.video_name` |
| video | [[!UICONTROL Asset ID]](/help/reporting/dimensions/asset-id.md) | `xdm.<_sandbox>.asset_id` |
| video | [[!UICONTROL First Air Date]](/help/reporting/dimensions/first-air-date.md) | `xdm.<_sandbox>.first_air_date` |
| video | [[!UICONTROL First Digital Date]](/help/reporting/dimensions/first-digital-date.md) | `xdm.<_sandbox>.first_digital_date` |
| video | [[!UICONTROL Content Rating]](/help/reporting/dimensions/content-rating.md) | `xdm.<_sandbox>.content_rating` |
| video | [[!UICONTROL Originator]](/help/reporting/dimensions/originator.md) | `xdm.<_sandbox>.originator` |
| videoad | ID chiave/annuncio | `xdm.<_sandbox>.key` |
| videoad | [[!UICONTROL Ad Length]](/help/reporting/dimensions/ad-length.md) | `xdm.<_sandbox>.ad_length` |
| videoad | [[!UICONTROL Ad Name]](/help/reporting/dimensions/ad-name.md) | `xdm.<_sandbox>.ad_name` |
| videoad | [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md) | `xdm.<_sandbox>.creative_id` |
| videoadpod | ID chiave/pod annuncio | `xdm.<_sandbox>.key` |
| videoadpod | [[!UICONTROL Pod Position]](/help/reporting/dimensions/pod-position.md) | `xdm.<_sandbox>.pod_position` |
| videoadpod | [[!UICONTROL Pod Name]](/help/reporting/dimensions/pod-name.md) | `xdm.<_sandbox>.pod_name` |
| videochapter | Chiave/Capitolo | `xdm.<_sandbox>.key` |
| videochapter | [[!UICONTROL Chapter Length]](/help/reporting/dimensions/chapter-length.md) | `xdm.<_sandbox>.chapter_length` |
| videochapter | [[!UICONTROL Chapter Offset]](/help/reporting/dimensions/chapter-offset.md) | `xdm.<_sandbox>.chapter_offset` |
| videochapter | [[!UICONTROL Chapter Position]](/help/reporting/dimensions/chapter-position.md) | `xdm.<_sandbox>.chapter_position` |
| videochapter | [[!UICONTROL Chapter Name]](/help/reporting/dimensions/chapter-name.md) | `xdm.<_sandbox>.chapter_name` |

## Variabili personalizzate di Media Analytics

In Adobe Analytics, le variabili personalizzate vengono assegnate a eventi o eVar diversi a seconda delle regole di implementazione definite all’interno di ogni suite di rapporti. Di conseguenza, quando queste variabili personalizzate vengono importate in Adobe Experience Platform (AEP), vengono mappate su percorsi XDM diversi.

* Gli eventi sono memorizzati nel percorso:

  `_experience.analytics.event<x>to<y>.event<number>.value`

* Le eVar sono memorizzate nel percorso:

  `_experience.analytics.customDimensions.eVars.eVar<number>`

In entrambi i casi, `<number>` corrisponde all&#39;evento specifico o al numero di eVar utilizzato nella configurazione originale della suite di rapporti di Adobe Analytics.

### Variabili personalizzate

| Nome campo: | Percorso XDM | Tipo di dati |
| --- | --- | --- |
| [[!UICONTROL Media Downloaded Flag]](/help/reporting/dimensions/media-downloaded-flag.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Metrica |
| Versione SDK | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensione |
| Versione libreria multimediale | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensione |
| [[!UICONTROL Stream Format]](/help/reporting/dimensions/stream-format.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensione |
| [[!UICONTROL First Air Date]](/help/reporting/dimensions/first-air-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensione |
| [[!UICONTROL First Digital Date]](/help/reporting/dimensions/first-digital-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensione |
| [[!UICONTROL Federated Data]](/help/reporting/metrics/federated-data.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>e<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Entrambi |
| [[!UICONTROL Estimated Streams]](/help/reporting/metrics/estimated-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Metrica |
| [[!UICONTROL Ad Count]](/help/reporting/metrics/ad-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Metrica |
| [[!UICONTROL Chapter Count]](/help/reporting/metrics/chapter-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Metrica |
| [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensione |
| [[!UICONTROL Site ID]](/help/reporting/dimensions/site-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensione |
| [[!UICONTROL Creative URL]](/help/reporting/dimensions/creative-url.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensione |
| [[!UICONTROL Placement ID]](/help/reporting/dimensions/placement-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensione |
| Frame al secondo | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>e<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Entrambi |
| ID errore SDK per contenuti multimediali | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Metrica |
| [[!UICONTROL Stalling Impacted Streams]](/help/reporting/metrics/stall-impacted-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Metrica |
| [[!UICONTROL Stalling Events]](/help/reporting/metrics/stall-events.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Metrica |
| [[!UICONTROL Total Stalling Duration]](/help/reporting/metrics/total-stalling-duration.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Metrica |
