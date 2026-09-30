---
title: Flussi interessati da picture in picture
description: Conta le sessioni in cui il visualizzatore è entrato nell'immagine nell'immagine almeno una volta.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 7%
---

# Flussi interessati da picture in picture

>[!BEGINSHADEBOX]

*In questa pagina sono inclusi i **Flussi interessati dalla metrica di generazione rapporti immagine nell&#39;immagine**. Per informazioni su come raccogliere questa variabile, vedere [Immagine nell&#39;immagine](/help/implementation/variables/player-state/picture-in-picture.md).*

>[!ENDSHADEBOX]

La metrica **Flussi interessati da immagine nell&#39;immagine** conta le sessioni in cui il visualizzatore è entrato almeno una volta nella riproduzione immagine nell&#39;immagine. La metrica è un valore booleano a livello di sessione; più voci picture-in-picture all’interno della stessa sessione vengono conteggiate come un flusso interessato. Per il volume totale di ingresso immagine nell&#39;immagine, utilizzare [Conteggi immagine nell&#39;immagine](picture-in-picture-count.md).

## Come è calcolata questa metrica

Il backend multimediale imposta questo flag la prima volta che viene ricevuto un evento di avvio dello stato immagine nell’immagine durante la sessione. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.states.pictureinpicture.set` quando [[!UICONTROL Player State Tracking]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | Voce [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/media-reporting-details) in cui `name = "pictureInPicture"`, campo `isSet` |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/it/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.set` |
