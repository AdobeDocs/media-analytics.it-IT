---
title: Fotogrammi saltati (quota)
description: Segnala il conteggio cumulativo di fotogrammi saltati per sessione.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 6%

---


# Fotogrammi saltati (quota)

>[!BEGINSHADEBOX]

*In questa pagina è inclusa la dimensione **Frame rilasciati**. Adobe Analytics compila automaticamente un [fotogramma saltato (metrica)](/help/reporting/metrics/dropped-frames.md) dalla stessa variabile di dati di contesto `a.media.qoe.droppedFrameCount`. Customer Journey Analytics espone un singolo campo `xdm.mediaReporting.qoeDataDetails.droppedFrames` che è possibile utilizzare come dimensione o come metrica. Per informazioni su come raccogliere questa variabile, vedere [Frame rilasciati](/help/implementation/variables/quality/dropped-frames.md).*

>[!ENDSHADEBOX]

La dimensione **Fotogrammi rilasciati** riporta il conteggio cumulativo dei fotogrammi saltati durante una sessione. Utilizza la dimensione per suddividere il coinvolgimento in base al numero esatto di rilasci.

## Compilazione di questa dimensione

Il lettore aggiorna il valore `droppedFrames` dell&#39;oggetto QoE mentre accumula le gocce. Il backend riporta il valore più recente nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.droppedFrameCount` quando [[!UICONTROL Media Quality]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `videoqoedroppedframecountevar`, `post_videoqoedroppedframecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

## Elementi dimensionali

Ogni elemento è il valore letterale di conteggio rilascio riportato nella chiamata di chiusura. Per il reporting booleano a livello di sessione (se sono stati eliminati dei fotogrammi), utilizza [Flussi interessati da fotogrammi saltati](/help/reporting/metrics/dropped-frame-impacted-streams.md).
