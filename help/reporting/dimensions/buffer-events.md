---
title: Eventi buffer (dimensione)
description: Riporta il numero di eventi di buffering per sessione.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 7%

---


# Eventi buffer (dimensione)

>[!BEGINSHADEBOX]

*In questa pagina sono inclusi **eventi buffer**. Adobe Analytics compila automaticamente un [evento buffer (metrica)](/help/reporting/metrics/buffer-events.md) associato dalla stessa variabile di dati di contesto `a.media.qoe.bufferCount`. Customer Journey Analytics espone un singolo campo `xdm.mediaReporting.qoeDataDetails.bufferCount` che è possibile utilizzare come dimensione o come metrica.*

>[!ENDSHADEBOX]

La dimensione **Eventi buffer** riporta il conteggio degli eventi di buffering che si sono verificati durante una sessione. Utilizza la dimensione per suddividere il coinvolgimento in base al numero esatto di buffer.

## Compilazione di questa dimensione

Il backend multimediale incrementa il conteggio ogni volta che il lettore entra in uno stato `buffer`. Il valore viene segnalato nella chiamata di chiusura.

| Sistema di reporting | Origine |
| --- | --- |
| Adobe Analytics | Raccolta automatica dai dati contestuali `a.media.qoe.bufferCount` quando [[!UICONTROL Media Quality]](/help/reporting/media-reports-enable.md) è abilitato. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feed di dati | `videoqoebuffercountevar`, `post_videoqoebuffercountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

## Elementi dimensionali

Ogni elemento è il valore letterale del conteggio dei buffer riportato nella chiamata di chiusura. Per il reporting booleano a livello di sessione (se la sessione ha riscontrato un buffering), utilizza [Flussi interessati dal buffer](/help/reporting/metrics/buffer-impacted-streams.md).
