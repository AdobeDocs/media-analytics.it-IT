---
title: Bitrate medio (metrica)
description: Segnala il bitrate medio ponderato non elaborato di ciascuna sessione, in kbps.
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
source-wordcount: '173'
ht-degree: 8%
---

# Bitrate medio (metrica)

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la metrica evento **Velocità in bit media**, che indica la media in bit rate non elaborato per sessione. Vedi [Bitrate medio (dimensione)](/help/reporting/dimensions/average-bitrate.md) per la dimensione a blocchi. Per informazioni su come raccogliere questa variabile, consulta [Bitrate](/help/implementation/variables/quality/bitrate.md).*

>[!ENDSHADEBOX]

La metrica **Velocità in bit media** riporta la velocità in bit media ponderata non elaborata di riproduzione, in kbps, per ogni sessione. A differenza della [dimensione a blocchi](/help/reporting/dimensions/average-bitrate.md), la metrica è un valore numerico continuo adatto a somme, medie e rollup percentili tra le sessioni.

## Come è calcolata questa metrica

Il backend multimediale calcola una media ponderata di tutti i valori di bitrate riportati durante la sessione, ponderata per la durata di attivazione di ogni bitrate. La metrica viene segnalata nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.bitrateAverage` quando [[!UICONTROL Media Quality]](/help/reporting/setup/analytics-reporting.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateAverage`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `event_list`, `post_event_list` (vedi ricerca [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateAverage` |
