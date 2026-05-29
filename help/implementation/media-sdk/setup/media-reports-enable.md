---
title: Abilitazione di rapporti sui contenuti multimediali
description: Scopri la suite di rapporti sui file multimediali che raccoglie le metriche sui file multimediali.  Per configurare i rapporti sui file multimediali prima dell’invio dei dati multimediali, effettua le seguenti operazioni.
uuid: d306068d-a308-4b6e-8a72-742dda0de428
exl-id: 686d88a5-79b6-4936-ba9e-8f834ef330d1
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/2nLLlF-rFJUR3t-OMbcy5iqF42l-O7oLybXFGhdPyhU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559id: e38cbddc-1633-4cd5-bed5-9f289f2a6029id: ef60b66e-5984-4336-ba72-6d978b1b6f87id: f1f1a2d4-0976-4881-b091-c2bb8de7ffacid: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 220
ht-degree: 40%

---

# Abilitazione di rapporti sui contenuti multimediali

Ogni suite di rapporti che raccoglie metriche multimediali deve essere configurata prima dell’invio dei dati multimediali.

1. In [Adobe Analytics](https://experience.adobe.com/analytics), passa a **[!UICONTROL Admin]** → **[!UICONTROL Report suites]**.
1. Seleziona le suite di rapporti che raccolgono dati multimediali. Selezionare **[!UICONTROL Edit Settings]** → **[!UICONTROL Media Management]** → **[!UICONTROL Media Reporting]**.

   ![Schermata del menu di Report Suite Manager](assets/media-reporting.png)

1. Nella pagina **[!UICONTROL Media Reporting]**, abilita i componenti multimediali di streaming desiderati (vedi di seguito).

1. Seleziona **[!UICONTROL Save].**

   Se questa suite di rapporti è già configurata per la raccolta dei dati multimediali, dopo aver fatto clic su **[!UICONTROL Save]**, viene visualizzata una pagina di configurazione aggiuntiva. Se vedi la pagina **[!UICONTROL Media Core measurement]**, continua con il passaggio successivo.

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
      * [!UICONTROL Ad loads]
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
