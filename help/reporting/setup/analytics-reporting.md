---
title: Configurare la generazione di rapporti per le implementazioni solo Analytics
description: Abilita i moduli suite per report multimediali in Adobe Analytics in modo che i dati multimediali in streaming possano essere raccolti e segnalati.
feature: Streaming Media
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 13%

---

# Configurare la generazione di rapporti per le implementazioni solo Analytics

Prima che un’implementazione basata solo su Analytics possa raccogliere dati multimediali in streaming, ogni suite di rapporti che riceve tali dati deve essere configurata per abilitare i moduli multimediali appropriati. Questa pagina descrive come abilitare tali moduli e dove trovare i rapporti risultanti.

* **Prerequisiti**: un&#39;implementazione Adobe Analytics. Consulta la [Panoramica sull&#39;implementazione di sola Analytics](/help/implementation/analytics-only/overview.md) e il metodo di implementazione scelto.

## Abilitare il reporting sui contenuti multimediali in una suite di rapporti

Ogni suite di rapporti che raccoglie metriche multimediali deve essere configurata prima dell’invio dei dati multimediali.

1. In [Adobe Analytics](https://experience.adobe.com/analytics), passa a **[!UICONTROL Admin]** → **[!UICONTROL Report suites]**.
1. Seleziona le suite di rapporti che raccolgono dati multimediali. Selezionare **[!UICONTROL Edit Settings]** → **[!UICONTROL Media Management]** → **[!UICONTROL Media Reporting]**.

   ![Schermata del menu di Report Suite Manager](assets/media-reporting.png)

1. Nella pagina **[!UICONTROL Media Reporting]**, abilitare i moduli di Streaming Media desiderati (vedere di seguito).

1. Seleziona **[!UICONTROL Save].**

   Se questa suite di rapporti è già configurata per la raccolta dei dati multimediali, dopo aver selezionato **[!UICONTROL Save]**, verrà visualizzata una pagina di configurazione aggiuntiva. Se vedi la pagina **[!UICONTROL Media Core measurement]**, continua con il passaggio successivo.

## Moduli multimediali in streaming disponibili

La misurazione dei file multimediali include i seguenti moduli:

* **[!UICONTROL Media Core]**: obbligatorio per il tracciamento di tutti i contenuti multimediali in streaming. Riserva le variabili della soluzione per la riproduzione dei contenuti e i dati di sessione.
   * **Dimensioni:**
      * [[!UICONTROL Content]](/help/reporting/dimensions/content.md)
      * [[!UICONTROL Content channel]](/help/reporting/dimensions/content-channel.md)
      * [[!UICONTROL Content length (variable)]](/help/reporting/dimensions/content-length.md)
      * [[!UICONTROL Content name (variable)]](/help/reporting/dimensions/content-name.md)
      * [[!UICONTROL Content player name]](/help/reporting/dimensions/content-player-name.md)
      * [[!UICONTROL Content segment]](/help/reporting/dimensions/content-segment.md)
      * [[!UICONTROL Content type]](/help/reporting/dimensions/content-type.md)
      * [[!UICONTROL Media path]](/help/reporting/dimensions/media-path.md)
      * [[!UICONTROL Media session ID]](/help/reporting/dimensions/media-session-id.md)
      * [[!UICONTROL Stream type]](/help/reporting/dimensions/stream-type.md)
   * **Metriche:**
      * [[!UICONTROL Average minute audience]](/help/reporting/metrics/average-minute-audience.md)
      * [[!UICONTROL Content completes]](/help/reporting/metrics/content-completes.md)
      * [[!UICONTROL Content resumes]](/help/reporting/metrics/content-resumes.md)
      * [[!UICONTROL Content segment views]](/help/reporting/metrics/content-segment-views.md)
      * [[!UICONTROL Content starts]](/help/reporting/metrics/content-starts.md)
      * [[!UICONTROL Content time spent]](/help/reporting/metrics/content-time-spent.md)
      * [[!UICONTROL Media starts]](/help/reporting/metrics/media-starts.md)
      * [[!UICONTROL Pause events]](/help/reporting/metrics/pause-events.md)
      * [[!UICONTROL Paused impacted streams]](/help/reporting/metrics/paused-impacted-streams.md)
      * [[!UICONTROL Progress markers]](/help/reporting/metrics/progress-markers.md)
      * [[!UICONTROL Total pause duration]](/help/reporting/metrics/total-pause-duration.md)
      * [[!UICONTROL Unique time played]](/help/reporting/metrics/unique-time-played.md)
* **[!UICONTROL Media Ads]**: abilita il tracciamento degli annunci all&#39;interno del contenuto multimediale.
   * **Dimensioni:**
      * [[!UICONTROL Ad]](/help/reporting/dimensions/ad.md)
      * [[!UICONTROL Ad in pod position]](/help/reporting/dimensions/ad-in-pod-position.md)
      * [[!UICONTROL Ad length (variable)]](/help/reporting/dimensions/ad-length.md)
      * [[!UICONTROL Ad name (variable)]](/help/reporting/dimensions/ad-name.md)
      * [[!UICONTROL Ad player name]](/help/reporting/dimensions/ad-player-name.md)
      * [[!UICONTROL Ad pod]](/help/reporting/dimensions/ad-pod.md)
      * [[!UICONTROL Advertiser]](/help/reporting/dimensions/advertiser.md)
      * [[!UICONTROL Campaign ID]](/help/reporting/dimensions/campaign-id.md)
   * **Dimensioni di classificazione:**
      * [[!UICONTROL Asset ID]](/help/reporting/dimensions/asset-id.md)
      * [[!UICONTROL Content rating]](/help/reporting/dimensions/content-rating.md)
      * [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md)
      * [[!UICONTROL First air date]](/help/reporting/dimensions/first-air-date.md)
      * [[!UICONTROL First digital date]](/help/reporting/dimensions/first-digital-date.md)
      * [[!UICONTROL Pod name]](/help/reporting/dimensions/pod-name.md)
      * [[!UICONTROL Pod position]](/help/reporting/dimensions/pod-position.md)
   * **Metriche:**
      * [[!UICONTROL Ad completes]](/help/reporting/metrics/ad-completes.md)
      * [[!UICONTROL Ad starts]](/help/reporting/metrics/ad-starts.md)
      * [[!UICONTROL Ad time spent]](/help/reporting/metrics/ad-time-spent.md)
      * [[!UICONTROL Media time spent]](/help/reporting/metrics/media-time-spent.md)
* **[!UICONTROL Media Chapters]**: abilita il tracciamento dei capitoli all&#39;interno del contenuto multimediale.
   * **Dimension:**
      * [[!UICONTROL Chapter]](/help/reporting/dimensions/chapter.md)
   * **Dimensioni di classificazione:**
      * [[!UICONTROL Chapter length]](/help/reporting/dimensions/chapter-length.md)
      * [[!UICONTROL Chapter name]](/help/reporting/dimensions/chapter-name.md)
      * [[!UICONTROL Chapter offset]](/help/reporting/dimensions/chapter-offset.md)
      * [[!UICONTROL Chapter position]](/help/reporting/dimensions/chapter-position.md)
      * [[!UICONTROL Originator]](/help/reporting/dimensions/originator.md)
   * **Metriche:**
      * [[!UICONTROL Chapter completes]](/help/reporting/metrics/chapter-completes.md)
      * [[!UICONTROL Chapter starts]](/help/reporting/metrics/chapter-starts.md)
      * [[!UICONTROL Chapter time spent]](/help/reporting/metrics/chapter-time-spent.md)
* **[!UICONTROL Media Quality]**: abilita il tracciamento dei dati di qualità della riproduzione, inclusi gli eventi di buffering, bitrate ed errore.
   * **Dimensioni:**
      * [[!UICONTROL Average bitrate]](/help/reporting/dimensions/average-bitrate.md)
      * [[!UICONTROL Bitrate changes]](/help/reporting/dimensions/bitrate-changes.md)
      * [[!UICONTROL Buffer events]](/help/reporting/dimensions/buffer-events.md)
      * [[!UICONTROL Dropped frames]](/help/reporting/dimensions/dropped-frames.md)
      * [[!UICONTROL Errors]](/help/reporting/dimensions/errors.md)
      * [[!UICONTROL External error IDs]](/help/reporting/dimensions/external-error-ids.md)
      * [[!UICONTROL Player SDK error IDs]](/help/reporting/dimensions/player-sdk-error-ids.md)
      * [[!UICONTROL Time to start]](/help/reporting/dimensions/time-to-start.md)
      * [[!UICONTROL Total buffer duration]](/help/reporting/dimensions/total-buffer-duration.md)
   * **Metriche:**
      * [[!UICONTROL Average bitrate]](/help/reporting/metrics/average-bitrate.md)
      * [[!UICONTROL Bitrate change impacted streams]](/help/reporting/metrics/bitrate-change-impacted-streams.md)
      * [[!UICONTROL Bitrate changes]](/help/reporting/metrics/bitrate-changes.md)
      * [[!UICONTROL Buffer events]](/help/reporting/metrics/buffer-events.md)
      * [[!UICONTROL Buffer impacted streams]](/help/reporting/metrics/buffer-impacted-streams.md)
      * [[!UICONTROL Dropped frame impacted streams]](/help/reporting/metrics/dropped-frame-impacted-streams.md)
      * [[!UICONTROL Dropped frames]](/help/reporting/metrics/dropped-frames.md)
      * [[!UICONTROL Drops before start]](/help/reporting/metrics/drops-before-start.md)
      * [[!UICONTROL Error events]](/help/reporting/metrics/error-events.md)
      * [[!UICONTROL Error impacted streams]](/help/reporting/metrics/error-impacted-streams.md)
      * [[!UICONTROL Time to start]](/help/reporting/metrics/time-to-start.md)
      * [[!UICONTROL Total buffer duration]](/help/reporting/metrics/total-buffer-duration.md)
* **[!UICONTROL Video Metadata]**: consente il tracciamento degli attributi di contenuto video standard come spettacolo, stagione e genere.
   * **Dimensioni:**
      * [[!UICONTROL Ad loads]](/help/reporting/dimensions/ad-load-type.md)
      * [[!UICONTROL Day part]](/help/reporting/dimensions/day-part.md)
      * [[!UICONTROL Episode]](/help/reporting/dimensions/episode.md)
      * [[!UICONTROL Genre]](/help/reporting/dimensions/genre.md)
      * [[!UICONTROL Media feed type]](/help/reporting/dimensions/media-feed-type.md)
      * [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md)
      * [[!UICONTROL Network]](/help/reporting/dimensions/network.md)
      * [[!UICONTROL Season]](/help/reporting/dimensions/season.md)
      * [[!UICONTROL Show]](/help/reporting/dimensions/show.md)
      * [[!UICONTROL Show type]](/help/reporting/dimensions/show-type.md)
   * **Metrica:**
      * [[!UICONTROL Authorized]](/help/reporting/metrics/authorized.md)
* **[!UICONTROL Audio Metadata]**: consente il tracciamento degli attributi di contenuto audio standard come artista, album e stazione.
   * **Dimensioni:**
      * [[!UICONTROL Album]](/help/reporting/dimensions/album.md)
      * [[!UICONTROL Artist]](/help/reporting/dimensions/artist.md)
      * [[!UICONTROL Author]](/help/reporting/dimensions/author.md)
      * [[!UICONTROL Label]](/help/reporting/dimensions/label.md)
      * [[!UICONTROL Publisher]](/help/reporting/dimensions/publisher.md)
      * [[!UICONTROL Station]](/help/reporting/dimensions/station.md)
* **[!UICONTROL Player State Tracking]**: consente la misurazione degli stati standard dell&#39;interfaccia utente del lettore, ad esempio schermo intero, sottotitoli e immagine nell&#39;immagine.
   * **Metriche:**
      * [[!UICONTROL Closed captioning counts]](/help/reporting/metrics/closed-captioning-count.md)
      * [[!UICONTROL Closed captioning total duration]](/help/reporting/metrics/closed-captioning-total-duration.md)
      * [[!UICONTROL Full screen counts]](/help/reporting/metrics/full-screen-count.md)
      * [[!UICONTROL Full screen total duration]](/help/reporting/metrics/full-screen-total-duration.md)
      * [[!UICONTROL In focus counts]](/help/reporting/metrics/in-focus-count.md)
      * [[!UICONTROL In focus total duration]](/help/reporting/metrics/in-focus-total-duration.md)
      * [[!UICONTROL Mute counts]](/help/reporting/metrics/mute-count.md)
      * [[!UICONTROL Mute total duration]](/help/reporting/metrics/mute-total-duration.md)
      * [[!UICONTROL Picture in picture counts]](/help/reporting/metrics/picture-in-picture-count.md)
      * [[!UICONTROL Picture in picture total duration]](/help/reporting/metrics/picture-in-picture-total-duration.md)
      * [[!UICONTROL Streams impacted by closed captioning]](/help/reporting/metrics/closed-captioning-streams-impacted.md)
      * [[!UICONTROL Streams impacted by full screen]](/help/reporting/metrics/full-screen-streams-impacted.md)
      * [[!UICONTROL Streams impacted by in focus]](/help/reporting/metrics/in-focus-streams-impacted.md)
      * [[!UICONTROL Streams impacted by mute]](/help/reporting/metrics/mute-streams-impacted.md)
      * [[!UICONTROL Streams impacted by picture in picture]](/help/reporting/metrics/picture-in-picture-streams-impacted.md)

>[!MORELIKETHIS]
>
>* [Report multimediali in Workspace](/help/reporting/workspace/media-workspace-templates.md)
>* [Panoramica delle dimensioni](/help/reporting/dimensions/overview.md)
>* [Panoramica delle metriche](/help/reporting/metrics/overview.md)
